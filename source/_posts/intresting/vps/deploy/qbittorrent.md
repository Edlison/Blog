---
title: deploy qbittorrent via docker
categories: 
- VPS
tags: 
- docker
---

# Intro

使用docker部署qbittorrent

<!--more-->

# Compose

```yaml
version: "3.3"

services:
  qbittorrent:
    image: linuxserver/qbittorrent
    container_name: qbittorrent
    environment:
      - PUID=0
      - PGID=0
      - TZ=Asia/Shanghai
      - WEBUI_PORT=10004
    volumes:
      - ./config:/config
      - ./downloads:/downloads
    ports:
      - 65535:65535
      - 65535:65535/udp
      - 10004:10004
```

