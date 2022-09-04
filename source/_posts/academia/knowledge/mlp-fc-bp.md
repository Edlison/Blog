---
title: Differences between MLP and FC and BP and FFN
categories:
- Academia
tags:
- mlp
- fc
- bp
---

# Intro

终极辨析MLP, FC, BP, FFN的关系

<!--more-->

# Diff

全连接网络(FullyConnected FC): 前一层每个神经元都与下一层的全部神经元连接. **这里强调只有一层**.

前馈网络(FeedForward FFN): 强调前向传播, 与RNN的同一层传播区别.

多层感知机(MultiLayerPerception MLP): 多个全连接网络(FC).

反向传播(BackPropagation BP): 用于降低loss.







全连接层是不包含激活函数的, 因此一般说带激活函数的全连接层.

只有使用了非线性的激活函数才能解决非线性问题, 否则仅使用全连接层是无法解决如XOR问题的.

> FFN=MLP=n * FC=n * Dense=n * relu(Wx+b)



---

References

https://www.cnblogs.com/zhangzheyang/p/10556572.html

https://www.zhihu.com/question/349854200

https://www.zhihu.com/question/476325700

https://ver217.github.io/2018/07/06/fc/

