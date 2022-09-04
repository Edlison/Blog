---
title: 根据PID查找启动路径
categories:
- Notebook
tags:
- linux
---

# Intro

根据PID查找进程启动路径

<!--more-->

# Method

## 法1

```sh
# /proc 目录下就是各进程的pid号
ls -ail /proc/pid
```

## 法2

```sh
lsof -p pid
```







---

Reference

https://www.cnblogs.com/pc-boke/articles/10012224.html