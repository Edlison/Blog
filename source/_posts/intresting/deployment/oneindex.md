---
title: Oneindex
categories: 
- VPS
tags: 
- oneindex
---

# Intro

使用docker搭建oneindex

调用Onedrive api的网盘, 不走服务器流量

<!--more-->

# Compose

```yaml
version: '3.9'

services:
  oneindex:
    image: setzero/oneindex
    volumes:
     - ./config:/var/www/html/config
     - ./cache:/var/www/html/cache
    ports:
     - 4000:80
    environment:
     - TZ='Asia/Shanghai'
     - REFRESH_TOKEN='0 * * * *'
     - REFRESH_CACHE='*/10 * * * *'
```

- `REFRESH_TOKEN`：使用crontab进行token更新，默认`0 * * * *`，即每小时更新一次
- `REFRESH_CACHE`：使用crontab进行缓存更新，默认`*/10 * * * *`，即每10分钟更新一次