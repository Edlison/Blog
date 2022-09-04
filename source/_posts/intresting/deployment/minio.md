---
title: deploy minio via docker
categories: 
- VPS
tags: 
- docker-compose
---

# Intro

搭建minio对象存储服务

<!--more-->

# Compose

```yaml
version: '3.3'

services:
  minio:
    image: bitnami/minio
    container_name: minio
    volumes:
      - ./data:/data
      - ./config:/root/.minio
    ports:
      - 9000:9000
      - 9001:9001
    environment:
      - MINIO_ACCESS_KEY=edlison
      - MINIO_SECRET_KEY=passwd
    privileged: true
```

# Official

## 单机

```yaml
version: '3.3'
services:
  minio:
    image: minio/minio
    container_name: minio
    ports:
      - 9000:9000 # api 端口
      - 9001:9001 # 控制台端口
    environment:
      MINIO_ACCESS_KEY: admin
      MINIO_SECRET_KEY: passwd
    volumes:
      - ./data:/data
      - ./config:/root/.minio
    command: server --console-address ':9001' /data  #指定容器中的目录
    privileged: true
```

## 集群

```yaml
version: '3'

# starts 4 docker containers running minio server instances.
# using nginx reverse proxy, load balancing, you can access
# it through port 9000.
services:
  minio1:
    image: minio/minio
    hostname: minio1
    volumes:
      - data1-1:/data1
      - data1-2:/data2
    expose:
      - "9000"
      - "9001"
    environment:
      MINIO_ROOT_USER: minio
      MINIO_ROOT_PASSWORD: minio123
    command: server --console-address ":9001" http://minio{1...4}/data{1...2}
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:9000/minio/health/live"]
      interval: 30s
      timeout: 20s
      retries: 3

  minio2:
    image: minio/minio
    hostname: minio2
    volumes:
      - data2-1:/data1
      - data2-2:/data2
    expose:
      - "9000"
      - "9001"
    environment:
      MINIO_ROOT_USER: minio
      MINIO_ROOT_PASSWORD: minio123
    command: server --console-address ":9001" http://minio{1...4}/data{1...2}
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:9000/minio/health/live"]
      interval: 30s
      timeout: 20s
      retries: 3

  minio3:
    image: minio/minio
    hostname: minio3
    volumes:
      - data3-1:/data1
      - data3-2:/data2
    expose:
      - "9000"
      - "9001"
    environment:
      MINIO_ROOT_USER: minio
      MINIO_ROOT_PASSWORD: minio123
    command: server --console-address ":9001" http://minio{1...4}/data{1...2}
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:9000/minio/health/live"]
      interval: 30s
      timeout: 20s
      retries: 3

  minio4:
    image: minio/minio
    hostname: minio4
    volumes:
      - data4-1:/data1
      - data4-2:/data2
    expose:
      - "9000"
      - "9001"
    environment:
      MINIO_ROOT_USER: minio
      MINIO_ROOT_PASSWORD: minio123
    command: server --console-address ":9001" http://minio{1...4}/data{1...2}
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:9000/minio/health/live"]
      interval: 30s
      timeout: 20s
      retries: 3

  nginx:
    image: nginx:1.19.2-alpine
    hostname: nginx
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
    ports:
      - "9000:9000"
      - "9001:9001"
    depends_on:
      - minio1
      - minio2
      - minio3
      - minio4

## By default this config uses default local driver,
## For custom volumes replace with volume driver configuration.
volumes:
  data1-1:
  data1-2:
  data2-1:
  data2-2:
  data3-1:
  data3-2:
  data4-1:
  data4-2:
```

# 永久访问





---

Reference

https://blog.csdn.net/weixin_40461281/article/details/118568289

https://www.cnblogs.com/blogCblog/p/14805044.html

https://www.cnblogs.com/CKExp/p/15605367.html