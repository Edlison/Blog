---
title: Javascript Starter
categories:
- JavaScript
---

# Intro

开始学习js

一些重要的概念

<!--more-->

# BOM

Broswer Object Model

小写的是对象, 大写的是类

对象

window 代表浏览器窗口(innerHeight...)

navigator 封装了浏览器的信息(userAgent...)

screen 代表屏幕尺寸(1920*1080)

location 代表当前页面的url信息(host, herf, ...)

document 当前页面信息(title, div, cookie, 动态修改页面, ...)

history 代表浏览器历史记录(页面前进后退)



# DOM

Document Object Model

浏览器网页就是一个DOM树形结构



操作

1. 得到

document.getElementById()

2. 更新

文本 doc.innerText('xxx')

CSS doc.style.color('red')

3. 删除

获取父节点, 然后删除

4. 添加

移动已经存在的: appendChild

创建新的: createElement, appendChild



# jQuery

$(selector).action()































