---
title: Nginx - load balance
categories:
- Nginx
tags:
- load_balance
---

# Intro

使用nginx进行负载均衡

<!--more-->

# Config

```nginx
http {
    upstream myapp1 {
        server srv1.example.com;
        server srv2.example.com;
        server srv3.example.com;
    }

    server {
        listen 80;

        location / {
            proxy_pass http://myapp1;
        }
    }
}
```

三种负载方式

- round-robin
- least-connected
- ip-hash







---

Reference

http://nginx.org/en/docs/http/load_balancing.html