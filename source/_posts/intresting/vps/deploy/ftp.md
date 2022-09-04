---
title: Deploy ftp via docker
categories:
- VPS
tags:
- docker
- ftp
---

# Intro

部署一个ftp服务

<!--more-->

# Compose

```yaml
version: "3.3"
services:
  ftp:
    image: fauria/vsftpd
    container_name: ftp
    environment:
      - FTP_USER=ftpuser
      - FTP_PASS=passwd
      - PASV_ADDRESS=127.0.0.1
      - PASV_MIN_PORT=21000
      - PASV_MAX_PORT=21010
    volumes:
      - ./data:/home/vsftpd
    ports:
      - 20:20
      - 21:21
      - 21000-21010:21000-21010
```

log文件夹不知道在哪

使用nginx实现http访问

```yaml
version: "3.3"
services:
  nginx:
    image: nginx
    container_name: nginx
    volumes:
      - ./config:/etc/nginx
      - ../ftp/data:/usr/share/nginx/html
      - ./logs:/var/log/nginx
    ports:
      - 80:80
    environment:
      - NGINX_PORT=80
```

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

  server {
        listen     80;
        server_name  ftp.edlison.com;

        location /{
                root /usr/share/nginx/html;
                autoindex  on;
                autoindex_exact_size off;
                autoindex_localtime on;
                charset utf-8,gbk;
        }
  }
}
```

# Config

```
# Run in the foreground to keep the container running:
background=NO

# Allow anonymous FTP? (Beware - allowed by default if you comment this out).
anonymous_enable=NO

# Uncomment this to allow local users to log in.
local_enable=YES

## Enable virtual users
guest_enable=YES

## Virtual users will use the same permissions as anonymous
virtual_use_local_privs=YES

# Uncomment this to enable any form of FTP write command.
write_enable=YES

## PAM file name
pam_service_name=vsftpd_virtual

## Home Directory for virtual users
user_sub_token=$USER
local_root=/home/vsftpd/$USER

# You may specify an explicit list of local users to chroot() to their home
# directory. If chroot_local_user is YES, then this list becomes a list of
# users to NOT chroot().
chroot_local_user=YES

# Workaround chroot check.
# See https://www.benscobie.com/fixing-500-oops-vsftpd-refusing-to-run-with-writable-root-inside-chroot/
# and http://serverfault.com/questions/362619/why-is-the-chroot-local-user-of-vsftpd-insecure
allow_writeable_chroot=YES

## Hide ids from user
hide_ids=YES

## Enable logging
xferlog_enable=YES
xferlog_file=/var/log/vsftpd/vsftpd.log

## Enable active mode
port_enable=YES
connect_from_port_20=YES
ftp_data_port=20

## Disable seccomp filter sanboxing
seccomp_sandbox=NO

### Variables set at container runtime
pasv_address=127.0.0.1
pasv_max_port=21010
pasv_min_port=21000
pasv_addr_resolve=NO
pasv_enable=YES
file_open_mode=0666
local_umask=077
xferlog_std_format=NO
reverse_lookup_enable=YES
pasv_promiscuous=NO
port_promiscuous=NO
```







---

https://hub.docker.com/r/fauria/vsftpd

https://www.cnblogs.com/djlsunshine/p/11164770.html

https://blog.csdn.net/qq_42881637/article/details/107357455