---
title: Nginx - request
categories:
- Nginx
tags:
- request
---

# Intro

Nginx处理请求

<!--more-->

# 根据域名路由服务器

```nginx
server {
    listen      80;
    server_name example.org www.example.org;
    ...
}

server {
    listen      80 default_server;
    server_name example.net www.example.net;
    ...
}
```

nginx仅通过Host字段对请求进行匹配, 然后对请求进行路由. 如果没有任何匹配的配置, 则会被转向`default_server`, 如果没有指定`default_server`则会被转向第一个`server`.

# 处理未定义的请求

```nginx
server {
    listen      80;
    server_name "";
    return      444;
}
```

如果请求头中的`Host`未被定义, 可以定义以上`server`去处理异常. **注意是未被定义, 而不是不匹配**.

# 混合名称和IP进行路由服务器

```nginx
server {
    listen      192.168.1.1:80;
    server_name example.org www.example.org;
    ...
}

server {
    listen      192.168.1.1:80 default_server;
    server_name example.net www.example.net;
    ...
}

server {
    listen      192.168.1.2:80 default_server;
    server_name example.com www.example.com;
    ...
}
```

listen可以指定ip, port, ip+port.

每个ip都可以有自己的`default_server`

# 一个简单的配置文件

```nginx
server {
    listen      80;
    server_name example.org www.example.org;
    root        /data/www;

    location / {
        index   index.html index.php;
    }

    location ~* \.(gif|jpg|png)$ {
        expires 30d;
    }

    location ~ \.php$ {
        fastcgi_pass  localhost:9000;
        fastcgi_param SCRIPT_FILENAME
                      $document_root$fastcgi_script_name;
        include       fastcgi_params;
    }
}
```

URL地址会被最具体的`location`规则所解析.







----

Reference

http://nginx.org/en/docs/http/request_processing.html