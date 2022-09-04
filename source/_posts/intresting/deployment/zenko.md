---
title: Deploy Zenko via docker
categories:
- Self-hosted
tags:
- docker
---

# Intro

部署Zenko基于S3协议的对象存储

<!--more-->

# Compose

```yml
version: '3.3'

services:
  zenko:
    image: zenko/cloudserver
    container_name: zenko
    volumes:
      - ~/app:/usr/src/app 
      - ~/pwd:/root/.aws
    environment:
      - ENDPOINT=s3.edlison.com
      - S3DATA=multiple
    ports:
      - 10011:8000
```

```sh
docker run -d --name CloudServer \
-v $(pwd)/data:/usr/src/app/localData -v $(pwd)/metadata:/usr/src/app/localMetadata \
-v $(pwd)/locationConfig.json:/usr/src/app/locationConfig.json \
-v $(pwd)/authdata.json:/usr/src/app/conf/authdata.json \
-v ~/.aws/credentials:/root/.aws/credentials -e S3DATA=multiple \
-e ENDPOINT=s3.edlison.com \
-p 8000:8000 -d zenko/cloudserver \
```

