---
title: Deploy CloudDrive
categories: 
- VPS
tags: 
- clouddrive
- self-hosted
---

# Intro
部署CloudDrive

<!--more-->

# Compose

```yml
version: "2.1"

services:
  cloudnas:
    image: cloudnas/clouddrive
    container_name: clouddrive
    volumes:
      - ./data:/CloudNAS:shared
      - ./config:/Config
      - ./media:/media:shared #optional media path of host
    devices:
      - /dev/fuse:/dev/fuse
    restart: unless-stopped
    pid: "host"
    privileged: true #or you can try capp_add -SYS_ADMIN
    #cap_add: #SYS_ADMIN cap may fail on some OSes, use privileged: true instead
    # - SYS_ADMIN
    network_mode: "host" #if network_mode doesn't work, use port mapping
    ports:
      - 9798:9798
```