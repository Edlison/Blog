---
title: Paper | INDUCTIVE REPRESENTATION LEARNING ON TEMPORAL GRAPHS
categories:
- Academia
tags:
- GNN
---

# Intro

TGAT

GraphSAGE + GAT + Time Encoding

每一层都是一个GAT，聚合的方式是使用了GraphSAGE，然后引入了一个Time Encoding获取时间信息。



# Methodology

## Time Encoding

取$|t-t_n|$时间差作为输入



## TGAT Layer

![](https://i.imgur.com/YQwMxcK.png)



![](https://i.imgur.com/Zm8lqEo.png)



层数就是聚合k-hop

**TGAT是根据跳数来分层计算的，不是根据时间。**

在第2层中：h0由h1, h2, h3获得

在第1层中：h1由h4, h5获得

**过程**

q关注当前v0节点，K, V关注上一级节点

通过attention和FFN获得最终h0







---

Reference

https://blog.csdn.net/weixin_42142630/article/details/116527314