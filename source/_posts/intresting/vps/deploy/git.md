---
title: Deploy git
categories: 
- VPS
tags: 
- self-hosted
---

# Intro

自建git

<!--more-->

# 方案

1. ssh协议: 直接通过具有权限的ssh用户即可搭建服务端, 并访问.

2. http协议: gitweb

# ssh

新建git用户

把现有仓库导出为裸仓库 一个不包含当前工作目录的仓库

```sh
git clone --bare my_project my_project.git
```

或新建一个裸仓库

```sh
mkdir ~/test.git
cd ~/test.git
git init --bare
```

通过git用户使用ssh协议访问

```sh
git push git@git.edlison.com:test.git
```

# web

```yaml
version: "3.3"

services:
  gitweb:
    image: fraoustin/gitweb
    container_name: gitweb
    environment:
      - CONTAINER_TIMEZONE=Asia/Shanghai
      - GITPROJECT=test
      - GITUSER=edlison
      - GITPASSWORD=passwd
    volumes:
      - ./data:/var/lib/git
    ports:
      - 10009:80
```

apache配置文件

```sh
root@aa6a6425e632:/# cat /etc/apache2/conf-available/gitweb.conf
<IfModule mod_alias.c>
  <IfModule mod_mime.c>
    <IfModule mod_cgi.c>
      Define ENABLE_GITWEB
    </IfModule>
    <IfModule mod_cgid.c>
      Define ENABLE_GITWEB
    </IfModule>
  </IfModule>
</IfModule>

<IfDefine ENABLE_GITWEB>
  Alias /gitweb /usr/share/gitweb

  <Directory /usr/share/gitweb>
    Options +FollowSymLinks +ExecCGI
    AddHandler cgi-script .cgi
  </Directory>
</IfDefine>
```

容器内指令

```
addrepos: add repository
addauth : add user for git
rmrepos : remove repository
rmauth : remove user
```







---

Reference

https://git-scm.com/book/zh/v2

https://hub.docker.com/r/fraoustin/gitweb