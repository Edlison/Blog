---
title: deploy vaultwarden via docker
categories:
- VPS
tags:
- docker-compose
---

# Intro

自建密码管理系统VaultWarden

<!--more-->

# Compose

```yaml
version: '3.3'

services:
  vaultwarden:
    image: vaultwarden/server
    container_name: vaultwarden
    environment:
      - ADMIN_TOKEN=your_random_token_gen_by_openssl_rand
      - DOMAIN=https://vaultwarden.edlison.com
    volumes:
     - ./data:/data
    ports:
     - 10006:80
```

# Settings

## admin page

> To enable the admin page, you need to set an authentication token. This token can be anything, but it's recommended to use a long, randomly generated string of characters, for example running `openssl rand -base64 48`. **Keep this token secret, this is the password to access the admin area of your server!**

To set the token, use the `ADMIN_TOKEN` variable:

```
ADMIN_TOKEN=your_random_token_gen_by_openssl_rand
```

## domain

Make sure to set the `DOMAIN` environment variable (or `domain` in the config file) to the URL you use to access your vaultwarden instance. If you don't, it's likely that various functionality will break mysteriously. Some examples:

```
DOMAIN=https://vaultwarden.edlison.com
```

# 注意

必须要https







---

Reference

https://github.com/dani-garcia/vaultwarden/wiki

https://hub.docker.com/r/vaultwarden/server

https://sspai.com/post/61694