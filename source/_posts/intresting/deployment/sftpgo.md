---
title: Deploy sftpgo via docker
categories:
- VPS
tags:
- self-hosted
---

# Intro

自建sftpgo

<!--more-->

# Compose

```yaml
version: '3.3'

services:
  sftpgo:
    image: drakkan/sftpgo
    container_name: sftpgo
    environment:
      - SFTPGO_FTPD__BINDINGS__0__PORT=10021
      - SFTPGO_FTPD__BINDINGS__0__FORCE_PASSIVE_IP=45.45.218.83
      - SFTPGO_FTPD__PASSIVE_PORT_RANGE__START=20020
      - SFTPGO_FTPD__PASSIVE_PORT_RANGE__END=20021
      - SFTPGO_WEBDAVD__BINDINGS__0__PORT=10011
    volumes:
      - data:/srv/sftpgo
      - config:/var/lib/sftpgo
    ports:
      - 10010:8080
      - 10011:10011
      - 10021:10021
      - 10022:2022
      - 20020-20021:20020-20021
volumes:
  data:
  config:
```

默认的ftp被动端口开的太多了, 每个监听的端口大概占0.9M的内存.



# Config

一共有4个服务

filesystem: 访问`10010`端口进入sftpgo的web界面

webdav: 访问`10011`端口

ftp: 访问`10021`端口

sftp: 访问`10022`端口

端口`20020-20021`是ftp的被动连接端口



ftp, sftp无法通过http访问







---

References

https://github.com/drakkan/sftpgo

