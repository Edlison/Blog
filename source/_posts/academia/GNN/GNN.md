---
title: 开始学习GNN
categories:
- Academia
tags:
- GNN
---

# Intro

A Gentle Introduction to Graph Neural Networks

<!--more-->

# Graph

V: Vertex attributes

E: Edge attributes and directions

U: Globle attributes

## 在图片上定义图

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20211220192722.png)

# Graph Neural Network

## simplest GNN

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20211220193102.png)

最简单的GNN, 分别在U, V, E三个层级上构建MLP

这种简单的结构并没有用到Graph的连接信息

## Pooling

比如说在分类问题下

如果V没有我们需要的信息, 可以用与之相连的E来表示, 反之亦然.

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20211220194530.png)

Link prediction 比如推荐系统

Node classification 比如用户

Graph classification 全局 比如分子结构

## Passing message

- 每个节点获取相邻节点的embedding
- (sum, mean, max)这些features
- 前向传播到nn

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20211220195224.png)

GCN也就是不断Pooling后作为该节点update后的feature, 相邻1节点, 相邻2节点...

## Representations

V的特征可以从临V或临E提取, 以及U.

E的特征也是.

U的特征也是.

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20211220195545.png)

A: adjacent matrix

X: feature matrix/attribute matrix 节点特征

W: weight matrix(update)

# 本质

GNN网络的本质是学习V, E, U的特征, 然后再进行分类等操作.

# 假设

CNN: 空间变换不变性

RNN: 时序的延续性

GNN: 图的对称性, 交换顶点GNN对其作用不变

# Survey

A Comprehensive Survey on Graph Anomaly Detection with Deep Learning

A Comprehensive Survey on Graph Neural Networks

Graph Learning: A Survey









---

References

https://distill.pub/2021/gnn-intro/

https://www.bilibili.com/video/BV1iT4y1d7zP