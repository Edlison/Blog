---
title: matplotlib理解
categories:
- Academia
tags:
- matplotlib
---

# Intro

一些对于matplotlib新的理解

<!--more-->

# Plot

plt: 返回的是一个`ax`, 相当于`plt.subplot()`

plt.subplot(): 返回的是一个`ax`, 整个画布就是一个`ax`

plt.subplots(row,col): 返回的是一个`fig`和一个`axes`. `fig`对画布操作, `axes`则包含了所有预定义的坐标轴.

plt.figure(): 返回的是一个`fig`空画布. 添加坐标轴需要`fig.add_subplot(row,col)`



