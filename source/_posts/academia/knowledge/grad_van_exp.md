---
title: 梯度消失&梯度爆炸
catagories:
- Academia
tags:
- vanish
---

# Intro

深度学习中梯度消失与梯度爆炸问题

<!--more-->

# Vanishing Gradient

比如在MLP中, 我们选择Sigmoid函数(也叫Logistic函数)作为激活函数.

![](https://i.imgur.com/8P6QVxb.png)
$$
S(x) = {1\over{1+e^{-x}}}
$$

$$
S'(x) = S(x)(1-S(x))
$$

反向转播时, 如果层数越深, 那么浅层的权重在计算梯度时就会越小.

因为Sigmoid函数值落在(0, 1)区间, 有多少层就会有多少个S'参与到梯度的计算.

# Exploding Gradient

反向传播过程中, 每一层的Loss梯度值持续超过1, 如果层数很深, 浅层的权重更新的梯度就会非常大.



---

References

https://zhuanlan.zhihu.com/p/38085620

https://www.jiqizhixin.com/articles/2017-12-21-14