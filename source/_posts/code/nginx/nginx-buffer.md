---
title: Nginx - buffer
categories:
- Nginx
tags:
- buffer
---

# Intro

对代理进行缓存

<!--more-->

# Config

```nginx
location / {
    proxy_pass       http://localhost:8000;
    proxy_set_header Host      $host;
    proxy_set_header X-Real-IP $remote_addr;
}
```

## 开关

```nginx
proxy_buffering on|off
```

开启后才会使缓冲区配置生效

## 缓冲区

```nginx
proxy_buffers 256 8k
```

设置缓冲区数量和大小

```nginx
proxy_buffer_size 8k
```

设置缓冲区大小

```nginx
proxy_bind $remote_addr transparent;
```

连接出口绑定为用户真实ip而非本机ip







----

Reference

http://nginx.org/en/docs/http/ngx_http_proxy_module.html