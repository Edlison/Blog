---
title: CSGO Dedicated Server CM2Network
categories:
- Game
tags:
- csgo
---

# Intro

部署一个私人CSGO服务器

<!--more-->

# Prerequisition

最低5Mbps可以10人默认竞技模式.

# Compose

```yaml
version: "3.9"

services:
  csgoserver:
    container_name: csgoserver
    image: cm2network/csgo:sourcemod
    environment:
      - SRCDS_TOKEN=token
      - SRCDS_RCONPW="password"
      - SRCDS_PW="" 
      - SRCDS_PORT=27015
      - SRCDS_TV_PORT=27020
      - SRCDS_NET_PUBLIC_ADDRESS="0"
      - SRCDS_IP="0"
      - SRCDS_FPSMAX=300
      - SRCDS_TICKRATE=128
      - SRCDS_MAXPLAYERS=10
      - SRCDS_STARTMAP="de_dust2"
      - SRCDS_REGION=4
      - SRCDS_MAPGROUP="mg_active"
      - SRCDS_GAMETYPE=0
      - SRCDS_GAMEMODE=1
      - SRCDS_HOSTNAME="NCEPU"
      - SRCDS_WORKSHOP_START_MAP=0
      - SRCDS_HOST_WORKSHOP_COLLECTION=0
      - SRCDS_WORKSHOP_AUTHKEY=""
      - ADDITIONAL_ARGS=""
    network_mode: host
```

# Config

获取op权限

```
rcon_password yourpasswd
```

之后的命令前加`rcon`即可作为server发出指令

```
rcon say hello
```

添加用户到`SourceMod`插件

```sh
echo '"id" "99:z"' >> csgo/addons/sourcemod/configs/admins_simple.ini
```

添加地图

- 创建一个创意工坊合集
- 把想玩的地图加到合集
- config中必须`SRCDS_WORKSHOP_START_MAP`和`SRCDS_HOST_WORKSHOP_COLLECTION` 同时存在

# Problem

不能`-v`挂载

```
csgoserver  |  Update state (0x81) verifying update, progress: 98.26 (30533132919 / 31072791505)
csgoserver  | Success! App '740' fully installed.
csgoserver  | tar: /home/steam/csgo-dedicated/csgo: Cannot open: No such file or directory
csgoserver  | tar: Error is not recoverable: exiting now
csgoserver  | tar: /home/steam/csgo-dedicated/csgo: Cannot open: No such file or directory
csgoserver  | tar: Error is not recoverable: exiting now
csgoserver  | tar: /home/steam/csgo-dedicated/csgo: Cannot open: No such file or directory
csgoserver  | tar: Error is not recoverable: exiting now
csgoserver  | sed: can't read /home/steam/csgo-dedicated/csgo/cfg/server.cfg: No such file or directory
csgoserver  | bash: /home/steam/csgo-dedicated/srcds_run: No such file or directory
csgoserver exited with code 127
```

每次compose up都默认执行了Dockerfile的CMD