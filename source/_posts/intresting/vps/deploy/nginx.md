---
title: nginx
categories: 
- VPS
tags: 
- linux
- ubuntu
- nginx
---

# docker compose

```yaml
version: '3.9'

services:
  nginx:
    image: nginx
    volumes:
     - ./html:/usr/share/nginx/html
     - ./config:/etc/nginx
     - ./logs:/var/log/nginx
     - ./www:/etc/www
    ports:
     - 80:80
    environment:
     - NGINX_HOST=edlison.com
     - NGINX_PORT=80
```

# config

```nginx
worker_processes  1;

events {
   accept_mutex on;
   multi_accept on;
   worker_connections 1024;
}

http {

server{
  listen 80;
  server_name  edlison.com www.edlison.com;

  location / {
	  root	/usr/share/nginx/html;
	  index	index.html;
  }
}

server{
  listen 80;
  server_name  v2ray.edlison.com;

  location / {
            proxy_set_header X_Real_IP $remote_addr;
            proxy_set_header X-Forwarded-For $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header Host $host;
      proxy_pass http://107.172.102.205:2000;
  }
}

server{
  listen 80;
  server_name  aria2.edlison.com;

  location / {
            proxy_set_header X_Real_IP $remote_addr;
            proxy_set_header X-Forwarded-For $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header Host $host;
      proxy_pass http://107.172.102.205:6880;
  }
}
  
server{
  listen 80;
  server_name  lib.edlison.com;

  location / {
            proxy_set_header X_Real_IP $remote_addr;
            proxy_set_header X-Forwarded-For $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header Host $host;
      proxy_pass http://107.172.102.205:11000;
  }
}

}
```

# 端口转发

`proxy_pass`放在最后

# 分网站配置

```
include
```