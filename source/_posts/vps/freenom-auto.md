---
title: freenom auto renew
categories:
- VPS
tags:
- docker
- domain
---

# compose

```yaml
version: "3.9"

services:
  Freenom-auto:
    container_name: freenom-auto
    image: luolongfei/freenom
    volumes:
      - ./config:/conf
      - ./logs:/app/logs
    restart: always
```

# telegram bot

todo







----

Reference

https://github.com/luolongfei/freenom
