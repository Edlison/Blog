---
title: CSGO Dedicated Server 解决方案
categories:
- Game
tags:
- csgo
---

# Intro

比较了几种主流搭建方法, 都是Linux平台.

# Compare

## 纯Docker

[cm2network](https://hub.docker.com/r/cm2network/csgo/)

优点: 这个方法完全依据valve提供的工具, 玩家可以指定环境变量来迅速启动

缺点: 不灵活

## CSGO Server Launcher

[crazy-max](https://github.com/crazy-max/csgo-server-launcher)

好像是一个纯脚本, 提供了一个CLI工具.

## LinuxGSM

[csgoserver](https://linuxgsm.com/lgsm/csgoserver/)

提供了一个CLI工具

**Features**

- Backup
- Console
- Details
- Installer (SteamCMD)
- Monitor
- Alerts (Email, Pushbullet)
- Update (SteamCMD)
- Start/Stop/Restart server

# 方案

最终准备采取Docker+LinuxGSM的方案, 即隔离了环境, 方便移植, 也保留了足够的配置灵活性, 也很简单.

# 步骤

1. 安装steamcmd

这一步的`Dockerfile`参考了cm2network

2. 安装LinuxGSM



国内网络现状

![](https://s2.loli.net/2022/01/08/yYI4BmekKLl7tTC.png)

# Dockerfile

```dockerfile
FROM debian:buster-slim

ARG PUID=1000

ENV USER steam
ENV HOMEDIR "/home/${USER}"
ENV STEAMCMDDIR "${HOMEDIR}/steamcmd"

# Install, update & upgrade packages
# Create user for the server
# This also creates the home directory we later need
# Clean TMP, apt-get cache and other stuff to make the image smaller
# Create Directory for SteamCMD
# Download SteamCMD
# Extract and delete archive
RUN set -x \
	&& dpkg --add-architecture i386 \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends --no-install-suggests \
		lib32stdc++6=8.3.0-6 \
		lib32gcc1=1:8.3.0-6 \
		wget=1.20.1-1.1 \
		ca-certificates=20200601~deb10u2 \
		nano=3.2-3 \
		libsdl2-2.0-0:i386=2.0.9+dfsg1-1 \
		curl=7.64.0-4+deb10u2 \
		locales=2.28-10 \
	&& sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen \
	&& dpkg-reconfigure --frontend=noninteractive locales \
	&& useradd -u "${PUID}" -m "${USER}" \
        && su "${USER}" -c \
                "mkdir -p \"${STEAMCMDDIR}\" \
                && wget -qO- 'https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz' | tar xvzf - -C \"${STEAMCMDDIR}\" \
                && \"./${STEAMCMDDIR}/steamcmd.sh\" +quit \
                && mkdir -p \"${HOMEDIR}/.steam/sdk32\" \
                && ln -s \"${STEAMCMDDIR}/linux32/steamclient.so\" \"${HOMEDIR}/.steam/sdk32/steamclient.so\" \
		&& ln -s \"${STEAMCMDDIR}/linux32/steamcmd\" \"${STEAMCMDDIR}/linux32/steam\" \
		&& ln -s \"${STEAMCMDDIR}/steamcmd.sh\" \"${STEAMCMDDIR}/steam.sh\"" \
	&& ln -s "${STEAMCMDDIR}/linux32/steamclient.so" "/usr/lib/i386-linux-gnu/steamclient.so" \
	&& ln -s "${STEAMCMDDIR}/linux64/steamclient.so" "/usr/lib/x86_64-linux-gnu/steamclient.so" \
	&& apt-get remove --purge -y \
		wget \
	&& apt-get clean autoclean \
	&& apt-get autoremove -y \
	&& rm -rf /var/lib/apt/lists/*

# Switch to user
USER ${USER}

WORKDIR ${STEAMCMDDIR}

VOLUME ${STEAMCMDDIR}
```

```dockerfile
FROM steamcmd:latest

ENV APP csgo
ENV APPDIR "${HOMEDIR}/${APP}"

COPY linuxgsm.sh ${HOMEDIR}/

RUN mkdir ${APPDIR} && mv linuxgsm.sh ${APP} \
	&& ./csgoserver install

VOLUME ${APPDIR}

USER ${USER}

WORKDIR ${HOMEDIR}

EXPOSE 27015/tcp \
	27015/udp \
	27020/udp
```

```dockerfile
FROM debian:buster-slim

ARG PUID=1000

ENV USER steam
ENV HOMEDIR "/home/${USER}"
ENV STEAMCMDDIR "${HOMEDIR}/steamcmd"


```



`entry.sh` 

```shell
#!/bin/bash
mkdir -p "${STEAMAPPDIR}" || true  

bash "${STEAMCMDDIR}/steamcmd.sh" +force_install_dir "${STEAMAPPDIR}" \
				+login anonymous \
				+app_update "${STEAMAPPID}" \
				+quit

# We assume that if the config is missing, that this is a fresh container
if [ ! -f "${STEAMAPPDIR}/${STEAMAPP}/cfg/server.cfg" ]; then
	# Download & extract the config
	wget -qO- "${DLURL}/master/etc/cfg.tar.gz" | tar xvzf - -C "${STEAMAPPDIR}/${STEAMAPP}"
	
	# Are we in a metamod container?
	if [ ! -z "$METAMOD_VERSION" ]; then
		LATESTMM=$(wget -qO- https://mms.alliedmods.net/mmsdrop/"${METAMOD_VERSION}"/mmsource-latest-linux)
		wget -qO- https://mms.alliedmods.net/mmsdrop/"${METAMOD_VERSION}"/"${LATESTMM}" | tar xvzf - -C "${STEAMAPPDIR}/${STEAMAPP}"	
	fi

	# Are we in a sourcemod container?
	if [ ! -z "$SOURCEMOD_VERSION" ]; then
		LATESTSM=$(wget -qO- https://sm.alliedmods.net/smdrop/"${SOURCEMOD_VERSION}"/sourcemod-latest-linux)
		wget -qO- https://sm.alliedmods.net/smdrop/"${SOURCEMOD_VERSION}"/"${LATESTSM}" | tar xvzf - -C "${STEAMAPPDIR}/${STEAMAPP}"
	fi

	# Change hostname on first launch (you can comment this out if it has done its purpose)
	sed -i -e 's/{{SERVER_HOSTNAME}}/'"${SRCDS_HOSTNAME}"'/g' "${STEAMAPPDIR}/${STEAMAPP}/cfg/server.cfg"
fi

# Believe it or not, if you don't do this srcds_run shits itself
cd "${STEAMAPPDIR}"

# Check if autoexec file exists
# Passing arguments directly to srcds_run, ignores values set in autoexec.cfg
autoexec_file="${STEAMAPPDIR}/${STEAMAPP}/cfg/autoexec.cfg"

# Overwritable arguments
ow_args=""

# If you need to overwrite a specific launch argument, add it to this loop and drop it from the subsequent srcds_run call
if [ -f "$autoexec_file" ]; then
        # TAB delimited name    default
        # HERE doc to not add extra file
        while IFS=$'\t' read -r name default
        do
                if ! grep -q "^\s*$name" "$autoexec_file"; then
                        ow_args="${ow_args} $default"
                fi
        done <<EOM
sv_password	+sv_password "${SRCDS_PW}"
rcon_password	+rcon_password "${SRCDS_RCONPW}"
EOM
	# if autoexec is present, drop overwritten arguments here (example: SRCDS_PW & SRCDS_RCONPW)
	bash "${STEAMAPPDIR}/srcds_run" -game "${STEAMAPP}" -console -autoupdate \
				-steam_dir "${STEAMCMDDIR}" \
				-steamcmd_script "${HOMEDIR}/${STEAMAPP}_update.txt" \
				-usercon \
				+fps_max "${SRCDS_FPSMAX}" \
				-tickrate "${SRCDS_TICKRATE}" \
				-port "${SRCDS_PORT}" \
				+tv_port "${SRCDS_TV_PORT}" \
				+clientport "${SRCDS_CLIENT_PORT}" \
				-maxplayers_override "${SRCDS_MAXPLAYERS}" \
				+game_type "${SRCDS_GAMETYPE}" \
				+game_mode "${SRCDS_GAMEMODE}" \
				+mapgroup "${SRCDS_MAPGROUP}" \
				+map "${SRCDS_STARTMAP}" \
				+sv_setsteamaccount "${SRCDS_TOKEN}" \
				+sv_region "${SRCDS_REGION}" \
				+net_public_adr "${SRCDS_NET_PUBLIC_ADDRESS}" \
				-ip "${SRCDS_IP}" \
				+host_workshop_collection "${SRCDS_HOST_WORKSHOP_COLLECTION}" \
				+workshop_start_map "${SRCDS_WORKSHOP_START_MAP}" \
				-authkey "${SRCDS_WORKSHOP_AUTHKEY}" \
				"${ow_args}" \
				"${ADDITIONAL_ARGS}"
else
	# If no autoexec is present, use all parameters
	bash "${STEAMAPPDIR}/srcds_run" -game "${STEAMAPP}" -console -autoupdate \
				-steam_dir "${STEAMCMDDIR}" \
				-steamcmd_script "${HOMEDIR}/${STEAMAPP}_update.txt" \
				-usercon \
				+fps_max "${SRCDS_FPSMAX}" \
				-tickrate "${SRCDS_TICKRATE}" \
				-port "${SRCDS_PORT}" \
				+tv_port "${SRCDS_TV_PORT}" \
				+clientport "${SRCDS_CLIENT_PORT}" \
				-maxplayers_override "${SRCDS_MAXPLAYERS}" \
				+game_type "${SRCDS_GAMETYPE}" \
				+game_mode "${SRCDS_GAMEMODE}" \
				+mapgroup "${SRCDS_MAPGROUP}" \
				+map "${SRCDS_STARTMAP}" \
				+sv_setsteamaccount "${SRCDS_TOKEN}" \
				+rcon_password "${SRCDS_RCONPW}" \
				+sv_password "${SRCDS_PW}" \
				+sv_region "${SRCDS_REGION}" \
				+net_public_adr "${SRCDS_NET_PUBLIC_ADDRESS}" \
				-ip "${SRCDS_IP}" \
				+host_workshop_collection "${SRCDS_HOST_WORKSHOP_COLLECTION}" \
				+workshop_start_map "${SRCDS_WORKSHOP_START_MAP}" \
				-authkey "${SRCDS_WORKSHOP_AUTHKEY}" \
				"${ADDITIONAL_ARGS}"
fi
```



---

References

https://github.com/CM2Walki/CSGO