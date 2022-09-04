---
title: Deploy Transmission via Docker
categories:
- Self-hosted
tags:
- transmission
---

# Intro

部署Transmission

<!--more-->

# Compose

```yaml
version: "3.3"
services:
  transmission:
    image: linuxserver/transmission
    container_name: transmission
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Asia/Shanghai
      - TRANSMISSION_WEB_HOME=/combustion-release/ #optional
      - USER=username #optional
      - PASS=password #optional
      - WHITELIST=iplist #optional
      - HOST_WHITELIST=dnsnane list #optional
    volumes:
      - ./config:/config
      - ~/Downloads:/downloads
      - ./watch:/watch
    ports:
      - 9091:9091
      - 65534:51413
      - 65534:51413/udp
    restart: unless-stopped
```

