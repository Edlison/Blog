---
title: cloudreve
categories:
- VPS
tags:
- cloudreve
---

# Intro

搭建Cloudreve

挂载OneDrive

连接Aria2

<!--more-->

# Cloudreve

使用docker compose部署

```yaml
version: '3'

services: 
    cloudreve: 
        image: xavierniu/cloudreve
        environment: 
            - TZ='Asia/Shanghai'
        ports:
            - 30000:5212
        volumes: 
            - ./uploads:/cloudreve/uploads
            - ./downloads:/downloads
            - ./config:/cloudreve/config
            - ./db:/cloudreve/db
            - ./avatar:/cloudreve/avatar
        networks: 
            - cloudreve-network

networks: 
    cloudreve-network:
```

# 挂载Onedrive

1. 添加存储策略
2. 根据提示添加Onedrive
3. 在`Azure Active Dictionary`中新建应用
4. 回调URI根据提示填写
5. 新建证书和密码
6. 验证后挂载成功

# 使用Aria2离线下载

1. 本机开一个aria2
2. Cloudreve连接

当Cloudreve转存完毕的时候自动删除下载的文件, 很方便, 不占用注意的存储

# 问题

1. 不知道内置数据库保存在哪了

# 大坑

Cloudreve离线下载指定的临时目录既是aria2的下载目录, 又是Cloudreve进行转存的目录.

因此docker挂载`Aria2`和`Cloudreve`的`/downloads`路径必须一致!!!









