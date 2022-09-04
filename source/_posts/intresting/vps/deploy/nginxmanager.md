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

