---
title: nginx ui
categories: 
- VPS
tags: 
- docker-compose
---

# Intro

Docker部署nginx-ui

nginx容器与nginx-ui容器连接

<!--more-->

# Compose

通过link两个容器减少暴露出来的端口

`expose`只会将端口暴露给

```yaml
version: "3.3"
services:
  nginx:
    image: nginx
    container_name: nginx
    volumes:
      - ./html:/usr/share/nginx/html
      - ./config:/etc/nginx
      - ./logs:/var/log/nginx
      - ./www:/etc/www
    ports:
      - 80:80
    environment:
      - NGINX_PORT=80
    links:
      - nginx-ui
    depends_on:
      - nginx-ui

  nginx-ui:
    image: schenkd/nginx-ui
    container_name: nginx-ui
    expose:
      - 8080
    volumes:
      - ./config:/etc/nginx
```

默认`nginx.conf`

```nginx
worker_processes  1;

events {
   accept_mutex on;
   multi_accept on;
   worker_connections 1024;
}

http {
  proxy_headers_hash_max_size 51200;
  proxy_headers_hash_bucket_size 6400;

  include conf.d/*.conf;


}

```



```nginx
worker_processes  1;

events {
   accept_mutex on;
   multi_accept on;
   worker_connections 1024;
}

http {
  server {
    listen          80;
    server_name     nginx.edlison.com;

    location / {
        auth_basic "Restricted Content";
        auth_basic_user_file .htpasswd;

        proxy_set_header X_Real_IP $remote_addr;
        proxy_set_header X-Forwarded-For $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $host;
        proxy_pass http://nginx-ui:8080;
    	}
		}
}
```

由于连接了两个容器 直接通过容器名连接

# 设置登录密码

```sh
touch .htpasswd
echo -n 'edlison:' >> .htpasswd
openssl passwd -apr1
```

# 配置生效

nginx在修改配置文件后需要手动重启

```sh
docker exec -it nginx nginx -t
```

# 注意

nginx需要`nginx.conf`文件在`/config`下

nginx-ui需要`conf.d`文件夹在`/config`下







---

Reference

https://cloud.tencent.com/developer/article/1358401
