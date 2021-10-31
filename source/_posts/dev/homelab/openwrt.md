---
title: Home Lab | OpenWRT
categories:
- Home Lab
tags:
- openwrt
---

# Intro

OpenWRT作为旁路由

# Process

## 安装

恩山论坛上有很多编译版本

通过scp上传到PVE的root目录下

使用`img2kvm`将镜像挂载到指定的虚拟机下

设置通过该镜像引导虚拟机

## 配置

配置IP到同一个子网下

```sh
vi /etc/config/network
```

重启后进入Web进行配置

设置接口

1. 网关指向iKuai
2. 关闭DHCP服务器

# 玩法

iKuai和OpenWRT的网关互指, 实现所有设备接入都可以hello world

iKuai网关指向自己, OpenWRT网关指向iKuai, 手动设置终端设备的router为OpenWRT, 可以实现分流

todo...

# 注意

ISO文件可以直接通过PVE面板上传至local, 然后虚拟机可以选择引导

img文件需要通过指令挂载, 文件格式的问题

PVE的noVNC管理工具是vim输入!

此时OpenWRT的接口相当于是在管理口上和iKuai的LAN口上

