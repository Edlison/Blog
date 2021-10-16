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
     - 2000:54321
     - 8000-8010:8000-8010/tcp
     - 8000-8010:8000-8010/udp
    tmpfs:
     - /tmp
     - /run
     - /run/lock
```

