---
title: lite v2ray via docker
categories: 
- VPS
tags: 
- linux
- ubuntu
- docker
- v2ray
---

# docker image

```sh
docker pull teddysun/v2ray
```

# docker compose

```yaml
version: '3.9'

services:
  v2ray:
    image: teddysun/v2ray
    restart: always
    volumes:
     - ./config:/etc/v2ray
    ports:
     - 9000:9000
```

# config.json

```json
{
  "inbounds": [{
    "port": 9000,
    "protocol": "vmess",
    "settings": {
      "clients": [
        {
          "id": "100xxxxx-xxxx-xxxx-xxxx-00xxxxxxxxxx",
          "level": 1,
          "alterId": 64
        }
      ]
    }
  }],
  "outbounds": [{
    "protocol": "freedom",
    "settings": {}
  }]
}
```

