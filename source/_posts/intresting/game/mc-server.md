---
title: Minecraft 搭建服务器
categories:
- Game
tags:
- Minecraft
---

# Intro

搭建Minecraft服务器

<!--more-->

# Java Server

[wiki](https://www.mcadmin.cn/start/bulid-and-config.html)

运行, 会自动下载所需文件.

```sh
java -Xms1G -Xms1G -jar server.jar
```

同意协议`eula` 

关闭官方验证`server.properties` 

```
online-mode=false
```

# MCManager

Dockerfile

```dockerfile
FROM node:latest
RUN mkdir -p /opt/mcsm \
	&& apt-get update && apt-get install openjdk-8-jdk -y \
	&& cd /opt/ \
	&& git clone https://github.com/suwings/mcsmanager \
	&& npm install --production
	
WORKDIR /opt/mcsm
CMD ["node", "app.js"]
```

Compose

```yaml
version: "3.2"

services:
  csgo:
    image: fuuko/mcmanager:latest
    container_name: mcmanager
    ports:
      - 20001:23333
      - 25565:25565
      - 25566:25566
    volumes:
      - ./mcsm:/app/MCSManager
```

注意: 这个镜像里用的是jdk1.8, 手动进去下载jdk17

# Resources

Server + MCSManager

大概占用1.3G RAM

每个用户大概占用0.2Mbps







---

References

https://cloud.tencent.com/developer/article/1631296

https://mcsmanager.com/

https://www.mcadmin.cn/

https://mcversions.net/