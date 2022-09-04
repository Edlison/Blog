---
title: 深度学习更新梯度的理解
categories:
- Academia
tags:
- grad
---

# Intro

自己对更新梯度的一点理解.

<!--more-->

# 偏导数是待更新权重在它方向上的变化率

前向传播其实就是一个很长的方程

$$
Loss = f(g(h(j(k(l(x))))))
$$

对权重求偏导数自然就要用到链式法则了, 从后向前求导(反向传播).

由于是对Wi求偏导数, 意味着是在Wi方向上的变化率, 对每一个更新的Wi都保证了在它们各自方向上的正确的梯度更新, 但是不保证对于整体是下降的.

# 更新梯度就是相当于在降低Wi方向上的Loss

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20220303205902.png)

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20220303211011.png)

无论是凸函数还是非凸函数, 总是会在Wi的方向上降低, 因为对于Wi的偏导包含了方向.

