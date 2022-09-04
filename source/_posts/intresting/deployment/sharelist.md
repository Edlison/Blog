---
title: sharelist via docker
categories: 
- VPS
tags: 
- docker
---

# Intro

使用docker搭建sharelist

<!--more-->

# Compose

```yaml
version: '3.3'

services:
  sharelist:
    image: reruin/sharelist
    container_name: sharelist
    volumes:
      - ./data:/app/cache
		ports:
		  - 10005:33001
```

# Config

挂载OneDrive

1. 使用OneDrive Business挂载: 输入分享url
2. 使用OneDrive API挂载: 进入Azure申请api

# 问题

容器内的`/app`文件夹映射不出来

OneDrive ID挂载不清楚从哪里获取ID

