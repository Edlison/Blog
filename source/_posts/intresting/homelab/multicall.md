---
title: iKuai 多播
categories:
- Home Lab
tags:
- iKuai
---

# Intro

使用iKuai进行多播

<!--more-->

# Settings

## 拨号

接入模式: 基于物理网卡的混合模式

PPPoE拨号: 添加账号

并发多播总数与添加账号数一致

## 负载均衡

流控分流 -> 多线负载

负载模式: 新建连接数

负载比例: 1:1...

# 注意

好像需要一次性新建4条线路

如果删除再添加好像不会叠加

# Results

做多4播成功

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20211121020933.png)







---

Reference

https://www.cnblogs.com/SavvyM/p/11653269.html