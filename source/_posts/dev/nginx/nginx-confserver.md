---
title: Nginx - Configure HTTPS servers
categories:
- Nginx
tags:
- https
---

# Intro

配置HTTPS服务器

<!--more-->

# Config

```nginx
server {
    listen              443 ssl;
    server_name         www.example.com;
    ssl_certificate     www.example.com.crt;
    ssl_certificate_key www.example.com.key;
    ssl_protocols       TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers         HIGH:!aNULL:!MD5;
    ...
}
```

证书会发给发送给所有用户

密钥保存在服务器本地

解析ssl证书会占用服务器资源

同一个ip只能绑定一个ssl证书, 这是由ssl机制决定的, 它先于http协议.







---

Reference

http://nginx.org/en/docs/http/configuring_https_servers.html