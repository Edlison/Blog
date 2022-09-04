---
title: 游戏加速解决方案
categories:
- Notebooks
tags:
- sstap
---

# Intro

自建游戏加速

V2ray + SSTap

<!--more-->

# Solution

游戏的流量一般走UDP协议, 因此V2ray只要打开UDP是可以代理游戏流量的.

但是V2ray的全局只是更改了系统内HTTP等协议的流量, 即使开启SOCKS5协议仍然无法代理游戏的流量.

SSTap的原理:

> 虚拟网卡，本地流量转发，再加路由规则







---

Reference

https://github.com/FQrabbit/SSTap-Rule

https://github.com/NetchX/Netch

http://ip111.cn/