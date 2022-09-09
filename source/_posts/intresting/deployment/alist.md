---
title: Deploy AList
categories: 
- VPS
tags: 
- alist
- self-hosted
---

# Intro

部署AList

<!--more-->

# Compose

```yaml
version: "3.3"

services:
  alist:
    image: xhofe/alist:latest
    container_name: alist
    volumes:
      - ./data:/opt/alist/data
    ports:
      - 11000:5244

```

# Config

Meta是对已经添加进来的所有账号进行管理，可以自定义目录密码，隐藏文件等。

----
Reference

https://alist-doc.nn.ci/docs/intro