---
title: Deploy Filezilla via docker
categories:
- VPS
tags:
- self-hosted
---

# Intro

搭建Docker container for FileZilla

<!--more-->

# Compose

```sh
docker run -d \
    --name=filezilla \
    -p 5800:5800 \
    -v /docker/appdata/filezilla:/config:rw \
    -v $HOME:/storage:rw \
    jlesage/filezilla
```

`$HOME`读取当前用户目录, 以便传输数据

注意权限管理, 以及搭建在内网上, 不然存储的服务器私钥会被获取.







---

Reference

https://registry.hub.docker.com/r/jlesage/filezilla