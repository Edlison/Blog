---
title: Deploy code-server on VPS
categories: 
- VPS
tags: 
- linux
- code-server
---

# compose

```yaml
version: "3.3"
services:
  code-server:
    image: lscr.io/linuxserver/code-server
    container_name: code-server
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - PASSWORD=password #optional
      - HASHED_PASSWORD= #optional
      - SUDO_PASSWORD=password #optional
      - SUDO_PASSWORD_HASH= #optional
      - PROXY_DOMAIN= #optional
    volumes:
      - ./config:/config
    ports:
      - 10005:8443
    restart: unless-stopped
```

[Linuxserver Doc](https://docs.linuxserver.io/images/docker-code-server)





