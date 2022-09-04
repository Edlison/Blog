---
title: Paper | Attention Plus
categories:
- Academia
tags:
- attention
---

# Intro

再理解Self-Attention

# Self-Attention

**Transformer**

![Transformer](https://i.imgur.com/p2Z0p4l.png)

**Self-Attention**

![Self-Attention](https://i.imgur.com/QaVJf6F.png)

**计算过程**

![](https://i.imgur.com/h1RBJra.png)

每一个输入首先分别通过一个线性变换, 输出Q, K, V

Q与所有其他位置的K进行dot-product(Additive等), 拿到相关性矩阵(A, Attention Matrix)

对这个矩阵进行softmax转化为概率(也可以通过一个激活函数ReLU等)

用A对每个输入的V矩阵乘, 就拿到了注意力后的vector

![](https://i.imgur.com/65s83f1.png)

![](https://i.imgur.com/gZx41Cw.png)

![](https://i.imgur.com/DB3Id6E.png)

![](https://i.imgur.com/1ffc0kc.png)

![](https://i.imgur.com/7iawt2Z.png)

# Multi-Head

![](https://i.imgur.com/XC4y6SD.png)

在分成多头的时候可以再加一组线性变换, 让可以学习的参数更多.

n个多头可以理解为有n种不同的相关性, 因此可以根据特定问题来进行改进.







---

References

https://www.youtube.com/watch?v=hYdO9CscNes

https://www.youtube.com/watch?v=gmsMY5kc-zw