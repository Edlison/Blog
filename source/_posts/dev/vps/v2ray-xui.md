---
title: x-ui for v2ray via docker
categories: 
- VPS
tags: 
- linux
- ubuntu
- docker
- v2ray
- x-ui
---

# docker image

```sh
docker pull thesadboy/x-ui
```

# docker compose

## for amd

```yaml
version: '3.9'

services:
  xui:
    image: thesadboy/x-ui
    restart: always
    volumes:
     - /sys/fs/cgroup:/sys/fs/cgroup:ro
     - ./config:/etc/x-ui
    ports:
     - 10001:54321
     - 8000-8010:8000-8010/tcp
     - 8000-8010:8000-8010/udp
    tmpfs:
     - /tmp
     - /run
     - /run/lock
```

## for amd and arm

```yaml
version: '3.7'
services:
  x-ui:
    image: stilleshan/x-ui
    container_name: x-ui
    restart: always
    network_mode: host
    volumes:
      - ./config:/etc/x-ui
      - ./ssl:/ssl
    ports:
     - 10001:54321
     - 20000-20010:20000-20010/tcp
     - 20000-20010:20000-20010/udp
```

