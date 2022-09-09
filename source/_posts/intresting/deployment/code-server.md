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

# Error: WebSocket close with status code 1006

使用Nginx进行代理时，登陆code-server会显示
```
An unexpected error occurred that requires a reload of this page.
The workbench failed to connect to the server (Error: WebSocket close with status code 1006)
```

可以在Nginx Manager中打开WebSockets Support，或者参考下面的文章。


# Terminal not showing

turn off `GPU acceleration` in `settings`

# Environment: Julia and Python

## Julia

Move compiled Julia to `./config/interpreter`

add julia path to system path.

## Python

Move source file to `./config/interpreter`

```bash
apt update

# isntall cpp lib
apt install gcc
apt install zlib*

# enter python direction
./configure

# make
make && make install

```

add python path to system path



----
References

https://blog.csdn.net/chszs/article/details/26369257
https://www.cnblogs.com/qianxunman/p/13656874.html