---
title: offline download solution
categories: 
- VPS
tags: 
- linux
- ubuntu
- aria2
- ariang
---

# aria2 ariang

## docker pull

```sh
docker pull p3terx/aria2
docker pull p3terx/ariang
```

## docker compose

```yaml
version: "3.3"

services:
  Aria2-Pro:
    container_name: aria2-pro
    image: p3terx/aria2-pro
    environment:
      - PUID=65534
      - PGID=65534
      - UMASK_SET=022
      - RPC_SECRET=GTX690
      - RPC_PORT=6800
      - LISTEN_PORT=6888
      - DISK_CACHE=512M
      - IPV6_MODE=false
      - UPDATE_TRACKERS=true
      - CUSTOM_TRACKER_URL=
      - TZ=Asia/Shanghai
    volumes:
      - ./config:/config
      - /mnt/slab/Downloads:/downloads
    network_mode: bridge
    ports:
      - 6800:6800
      - 6888:6888
      - 6888:6888/udp
    restart: unless-stopped
    logging:
      driver: json-file
      options:
        max-size: 1m

  AriaNg:
    container_name: ariang
    image: p3terx/ariang
    network_mode: bridge
    ports:
      - 10002:6880
    restart: unless-stopped
    logging:
      driver: json-file
      options:
        max-size: 1m
```

## config

```
cat ~/Applications/aria2/config/script.conf
```







----

Reference

https://p3terx.com/archives/docker-aria2-pro.html