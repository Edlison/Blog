---
title: Nginx - auth
categories:
- Nginx
tags:
- auth
---

# Intro

基于http协议的基础验证

<!--more-->

# Config

```nginx
location / {
    auth_basic           "closed site";
    auth_basic_user_file conf/.htpasswd;
}
```

设置密码

```sh
touch .htpasswd
echo -n 'edlison:' >> .htpasswd
openssl passwd -apr1
```







---

Reference

http://nginx.org/en/docs/http/ngx_http_auth_basic_module.html