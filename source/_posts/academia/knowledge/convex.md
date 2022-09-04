---
title: 凸函数 非凸函数
categories:
- Academia
tags:
- convex
---

# Intro

凸函数和非凸函数的区别

<!--more-->

# Definition

$$
f((x_1 + x_2)/2) \leq (f(x_1) + f(x_2))/2
$$

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20220303195737.png)

一般是指上方图是凸的.



# 机器学习中的凸与非凸

凸：

- 指的是顺着梯度方向走到底就 **一定是 最优解** 。
- **大部分 传统机器学习 问题** 都是凸的。

非凸：

- 指的是顺着梯度方向走到底只能保证是局部最优，**不能保证** 是全局最优。
- **深度学习**以及小部分传统[机器学习](https://so.csdn.net/so/search?q=机器学习&spm=1001.2101.3001.7020)问题都是非凸的。



# 为什么损失函数都是非凸的

> **一个高维凸函数可以等价于无数个一维凸函数的叠加。一个（高维）函数是凸的，当且仅当把这个函数限制到任意直线上它在定义域上仍然是凸的**。那只要我们找到一点 ，和一个“方向” ，使得这个函数非凸就可以了！回顾一维凸函数的定义，这就是说在这个方向上找到两个点，他们平均的函数值比他们平均值上的函数值要低就行了。

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20220303200458.png)



---

References

https://baike.baidu.com/item/%E5%87%B8%E5%87%BD%E6%95%B0/3371735

https://blog.csdn.net/jningwei/article/details/78836920

https://zhuanlan.zhihu.com/p/141542614