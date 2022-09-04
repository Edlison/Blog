---
title:  CSGO Dedicated Server CrazyMax
categories:
- Game
tags:
- csgo
---

# Intro

使用CrazyMax的launcher来部署

<!--more-->

# Compose

```yaml
version: "3.2"

services:
  csgo:
    image: crazymax/csgo-server-launcher:latest
    container_name: csgo
    ports:
      - target: 27015
        published: 27015
        protocol: udp
      - target: 27015
        published: 27015
        protocol: tcp
    env_file:
      - ".env"
    volumes:
      - "./csgo:/var/steamcmd/games/csgo"
      - "./steam:/home/steam/Steam"
    tty: true
    ulimits:
      nproc: 65535
      nofile:
        soft: 32000
        hard: 40000
    restart: always
```

# Config

`.env` 

```
TZ=Europe/Paris
PUID=1000
PGID=1000
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_TLS=on
SMTP_STARTTLS=on
SMTP_TLS_CHECKCERT=on
SMTP_AUTH=on
SMTP_USER=foo
SMTP_PASSWORD_FILE=bar
SMTP_FROM=foo@gmail.com
SMTP_DOMAIN=localhost

PORT=27015
GSLT=78E838FA2D03D46A5C2C83B53DCC2363
STEAM_LOGIN=anonymous
STEAM_PASSWORD=anonymous
UPDATE_EMAIL=
UPDATE_RETRY=3
CLEAR_DOWNLOAD_CACHE=0
#API_AUTHORIZATION_KEY=FB7B224C7A8BCE191EDBA77E2563D6E3
#WORKSHOP_COLLECTION_ID=2710395539
#WORKSHOP_START_MAP=2658774556
MAXPLAYERS=18
TICKRATE=128
EXTRAPARAMS=-nohltv +sv_pure 0 +game_type 0 +game_mode 0 +mapgroup mg_active +map de_dust2
```

