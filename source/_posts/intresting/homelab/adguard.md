---
title: Home Lab | AdGuard
categories:
- Home Lab
tags:
- openwrt
- adguard
---

# Intro

使用AdGuard屏蔽广告

iKuai + OpenWrt(AdGuard)

<!--more-->

# Settings

1. 在OpenWrt中打开AdGuard
2. 初始化用户
3. 设置登录端口`10000`
4. 设置DNS端口`5553`
5. 设置上游DNS服务器
6. 设置Bootstrap DNS服务器
7. 端口重定向

法一:

在OpenWrt中设置5553重定向至AdGuard

法二:

在OpenWrt中设置5553作为dnsmasq的上游服务器

在OpenWrt中设置防火墙规则

```
iptables -t nat -A PREROUTING -p udp --dport 53 -j REDIRECT --to-ports 5553
iptables -t nat -A PREROUTING -p tcp --dport 53 -j REDIRECT --to-ports 5553
```

6. 配置iKuai的DHCP服务

DNS指向OpenWrt

7. 添加过滤规则[link](https://www.iyio.net/2021/08/1714.html)



# 大坑

若打开AdGuard设置中的`家长控制`服务则会出现异常

# 注意

终端设备如果使用DHCP服务则会自动配置好DNS

终端设备如果手动配置, 需要将路由指向OpenWrt, 且配置DNS为OpenWrt的地址







---

References

https://cyhour.com/1403/

https://zhuanlan.zhihu.com/p/367840918

https://www.iyio.net/2021/08/1714.html