---
title: install docker and compose
categories: 
- VPS
tags: 
- linux
- docker
---

# engine

> https://docs.docker.com/engine/install/

```sh
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```



# compose

> https://docs.docker.com/compose/install/

```sh
apt install docker-compose
```



# 注意

docker安装完毕后会自动创建一个`docker ` group, 添加用户进入到该组, 否则每次执行指令都需要`sudo `权限.

```sh
sudo gpasswd -a $USER docker     	#将登陆用户加入到docker用户组中
newgrp docker     								#更新用户组
# 运行这个镜像测试docker的安装
docker run hello-world
# 如果出现权限问题 则是‘~/.docker/’目录收到了sudo权限的影响
sudo chown "$USER":"$USER" /home/"$USER"/.docker -R
sudo chmod g+rwx "$HOME/.docker" -R
```







---

Reference

https://docs.docker.com/engine/install/linux-postinstall/

https://blog.csdn.net/a1556274485/article/details/109991868
