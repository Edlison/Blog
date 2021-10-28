---
title: offline download solution
categories: 
- VPS
tags: 
- linux
---

# h5ai

## amd

h5ai realize static file could be shown online eazily

### docker compose

```yaml
version: "3.8"

services:
  h5ai:
    container_name: h5ai
    image: clue/h5ai
    volumes:
      - /mnt/GoogleDrive:/var/www
    ports:
      - 11000:80
```

## arm

### docker compose

```yaml
version: "3.3"

services:
  h5ai:
    container_name: h5ai
    image: awesometic/h5ai
    volumes:
      - /mnt/slab:/h5ai
      - ./config:/config
    environment:
      - HTPASSWD=true
      - HTPASSWD_USER=edlison
      - HTPASSWD_PW=youpw
      - TZ=Asia/Shanghai
    ports:
      - 10003:80
```

