---
title: nginx webui
categories: 
- VPS
tags: 
- linux
- nginx
---

# Intro



# compose

```yaml
version: "3.3"
services:
  nginxWebUi-server:
    image: yogile/nginxwebui-aarch64:latest
    volumes:
      - ./config:/home/nginxWebUI
    ports:
      - 80:80
      - 10000:8080
    environment:
      BOOT_OPTIONS: "--server.port=8080"
```

