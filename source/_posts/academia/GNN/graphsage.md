---
title: Paper | Inductive Representation Learning on Large Graphs
categories:
- Academia
tags:
- GNN
---

# Intro

GraphSAGE

大多数graph embedding框架是transductive（直推式的），只能对一个固定的图生成embedding。这种transductive的方法不能对图中没有的新节点生成embedding。

相对的，GraphSAGE是一个inductive（归纳式）框架，能够高效地利用节点的属性信息对新节点生成embedding。

<!--more-->

# Methodology

## Aggregate

![](https://i.imgur.com/srvtHjZ.png)

学的是一个Aggregator的方程



## Update

![](https://i.imgur.com/Yvcu4v4.png)

Update是先级联操作，然后通过一个线性变换。

由于级联改变了输入维度，W会进行一个降维操作。

每一个k-hop的W都不一样



> code: https://github.com/williamleif/graphsage-simple/







----

Reference

https://zhuanlan.zhihu.com/p/367741877