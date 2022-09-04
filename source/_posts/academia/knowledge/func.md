---
title: 常用函数整理
categories:
- Academia
tags:
- softmax
- sigmoid
---

# Intro

整理了一些常用的函数, 及他们的导数

<!--more-->

# Content

## logit (log-it)

$$
log({P\over{1-P}})=\beta_0+\beta_1x_1+...+\beta_nx_n
$$

## logistic

$$
y={1\over{1+e^{-x}}}
$$

当logit只考虑一个自变量时, 等式两边同时求e的次方, 就与logistic一样了.

这里讲的不严谨, 可以看ref

## sigmoid

也叫logistic
$$
y={1\over{1+e^{-x}}}
$$

$$
y'=y(1-y)
$$



![](https://i.imgur.com/8P6QVxb.png)

## softmax

$$
softmax(x)={e^{x_i}\over{\sum_{i=1}^N}e^{x_i}}
$$



![](https://i.imgur.com/UhwNq5v.png)



---

References

https://zhuanlan.zhihu.com/p/30659982

https://zhuanlan.zhihu.com/p/105722023