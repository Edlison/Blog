---
title: Deploy Nginx Proxy Manager
categories:
- Self-hosted
tags:
- docker
- nginx
---

# Intro

Nginx可视化

<!--more-->

# Compose

```yaml
version: "3"
services:
  app:
    image: 'jc21/nginx-proxy-manager:latest'
    restart: unless-stopped
    ports:
      - 80:80 # Public HTTP Port
      - 443:443 # Public HTTPS Port
      - 10000:81 # Admin Web Port
    volumes:
      - ./data:/data
      - ./letsencrypt:/etc/letsencrypt
```

# Static Website

If you want to configure a static website, follow the instructions below.

1. add a new `Proxy`
2. fill out `Domain name`, `Scheme`, `Forward hostname`(this won't be processed, just write 'localhost' is fine), `Port`.
3. add `Custom Configuration`

```Nginx
location / {
    root /data/nginx/default_www;
    index index.html;
}
```