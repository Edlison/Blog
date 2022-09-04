---
title: DockerApp - Redis
categories:
- Docker
tags:
- redis
---

# Intro

使用Docker部署Redis

<!--more-->

# Compose

```yaml
version: '3.1'

services:
  redis:
    image: redis
    container_name: redis
    restart: always
    ports:
      - 6379:6379
    volumes:
      - ./data:/data
      - ./conf/redis.conf:/etc/redis/redis.conf
    command: 
      /bin/bash -c "redis-server /etc/redis/redis.conf"
```

# 坑

`redis.conf`

```
bind * -::*

requirepass yourpassword
protected-mode no
daemonize no
```



`bind` 必须改成`*` 才可以远程访问