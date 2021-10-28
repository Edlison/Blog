---
title: homepage hook
categories: 
- VPS
tags: 
- linux
- webhook
---

# 方案

本地编译, 将编译好的文件上传git并且文件自动部署到nginx

todo: 后期将原文件上传git通过action自动编译并部署

## 思路1

本地push到github, 通过webhook发送POST请求到VPS, 执行shell进行clone然后拷贝至nginx

问题: 服务器需要处理http请求

## 思路2

本地同时push到VPS和github, VPS通过hook执行shell拷贝至nginx

问题: 同时push两个仓库感觉不是很优雅

# git

```sh
adduser git --ingroup sudo  # add user
```

```sh
mkdir ~/edlison/Home.git -p  # new user dir and git repo
```

copy local public key to git

```sh
git remote set-url sj git@sj:edlison/Home.git  # set push url
```

# hook

```sh
cd ~/edlison/Home.git/hooks
vim post-receive
```

```sh
echo "post-receive hook is running..."

GIT_REPO=/home/git/edlison/Home.git
TMP_GIT_CLONE=/tmp/homepage
PUBLIC_WWW=/home/ubuntu/Applications/nginx/html

rm -rf $TMP_GIT_CLONE
git clone $GIT_REPO $TMP_GIT_CLONE
rm -rf ${PUBLIC_WWW}/*
cp -rf ${TMP_GIT_CLONE}/* ${PUBLIC_WWW}/

echo "post-receive hook is done!"
```



----

References

https://sampwood.github.io/2018/10/17/vps-git-repo-ngxin-git-hook

http://yearito.cn/posts/hexo-deploy-to-VPS.html