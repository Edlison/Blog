---
title: Home Lab | iKuai
categories:
- Home Lab
tags:
- ikuai
---

# Intro

iKuai作为主路由

# Process

## 安装

[iKuai官网](https://www.ikuai8.com/)

上传镜像到PVE的local

注意内存要分配4G, 尝试了32位版本2G内存, 安装异常

配置两个网口eth0, eth1给iKuai

设置LAN地址, 要在一个子网下

## 配置

通过Web连接并配置

1. 将路由器设置为AP模式
2. 绑定eth0为WAN口, 把网线接入WAN口
3. 设置LAN口, 将虚拟机虚拟出来的LAN口和分配的eth1桥接
4. 设置DHCP服务器

**注意**

此时不可以将LAN口和原本的管理口都连入路由器, 会造成回环!

此时的LAN口和管理口相当于一样了

# 问题

mbp的hostname由于回环造成了路由器里有两个一样的设备

# 反思

网络的知识忘的差不多了

内网种只有在同一个子网才能访问到

**网关**相当于连接着多个子网, 一般来说就是路由器

但本质上是通过网关去找路由表, 可以把网关设为某个设备, 然后该设备再跳到真正的网关, 如iKuai作为网关且网关指向自己, OpenWRT网关指向iKuai, 如果路由设置为OpenWRT则流量先被OpenWRT接管, 如果网关直接指向iKuai则流量不会被OpenWRT接管.







----

