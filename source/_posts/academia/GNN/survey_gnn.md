---
title: A Comprehensive Survey on GNN
categories:
- Academia
tags:
- GNN
- survey
---

# Intro

A Comprehensive Survey on Graph Neural Networks 论文笔记

<!--more-->

# Abstract

数据在诸如CV和NLP领域用Euclidean来表示, 但是还有很多数据如用户关系等non-Euclidean可以用图来表示.

本篇论文将GNN大体分为Recurrent Graph Neural Networks, Convolutional Graph Neural Networks, Graph Autoencoders, Spatial-Temporal Graph Neural Networks四类.

并在之后会讲述SOTA模型, benchmark数据集, 实际应用, 以及未来方向.

# Background & Definition

**GNN vs Network embedding**

Network embedding 是用低维向量来表示网络节点, 保留了网络的拓扑结构以及节点信息. 随后可以使用传统的机器学习方法来进行classification等任务.

GNN 是深度学习模型, 旨在处理图相关的端到端任务.

区别在于Network embedding 包括一些非深度模型.

**GNN vs Graph kernel methods**

Graph kernel 可以将图或节点通过映射嵌入到向量.

Graph kernel 是直接定义的, 而不是通过网络学习.

# Categorization & Framework

**RecGNN**

图中的节点不断与邻居交换信息, 直到稳定.

**ConvGNN**

通过多个卷积层提取高阶节点表示

**GAE**

是一种无监督的框架. 将节点encode导隐空间, 然后在重建.

**STGNN**

同时考虑空间及时间.

## 框架

**任务**

- Node-level
- Edge-level
- Graph-level

**训练**

- Semi-supervised learning for node-level classification 只给部分节点打标签, 让网络学习去给unlabeled node打标签
- Supervised learning for graph-level classification 对整个图预测
- Unsupervised learning for graph embedding 探索edge-level的信息, 一种方式是用Autoencoder, 另一种方式是使用negative sampling, 取一些negative pairs, 图中出现的连接节点对是positive pairs.

# Recurrent Graph Neural Network

对节点循环应用相同的参数去提取特征.

一个节点的隐层状态由这个式子循环更新.
$$
h_v^{(t)} = \sum_{u\in N(v)}f(x_v, x^e_{(v, u)}, x_u, h_u^{(t-1)})\\
f = (Wx + b)
$$
传统的RNN

![](https://s2.loli.net/2022/01/03/dfoV2NOMFC7BkRU.png)

每一次计算包含, 当前节点, 邻居节点, 边的信息, 上一个隐层状态信息. 遍历完一个节点的所有邻居相加.

此时学到的h可作为当前节点的特征.

**Gated Graph Neural Network**
$$
h_v^{(t)} = GRU(h_v^{(t-1)}, \sum_{u\in N(v)}Wh_u^{(t-1)})
$$
**RecGNN和ConvGNN的区别**

![](https://s2.loli.net/2022/01/03/a6s9nT32cq51C8D.png)

# Convolutional Graph Neural Network

## Spectral-based ConvGNN

$$
L = I_n - D^{-{1\over2}}AD^{-{1\over2}}\\
D_{ii}=\sum_j(A_{ij})
$$

D是对角矩阵

## Spatial-based ConvGNN

### NN4G

直接相加节点的所有邻居信息, 还应用了residual connections 和 skip connections.

NN4G的下一层节点状态
$$
h_v^{(k)}=f(W^{(k)^T}x_v+\sum_{i=1}^{k-1}\sum_{u\in N(v)}\Theta^{(k)^T}h_u^{(k-1)})
$$
NN4G与GCN的区别是没有用正则化的邻接矩阵.

### DCNN(Diffussion CNN)

这个模型认为信息的传递有特定的概率, 几轮后会平衡.

### PGC-DGCNN

增加了远邻居的贡献, 定一个一个最短路径邻接矩阵S. 
$$
H^{(k)}=\Vert^r_{j=0}f((\tilde D^{(j)})^{-1}S^{(j)H^{(k-1)}}W^{(j,k)})\\
$$

### MPNN(Message Passing NN)

它将Conv视作一个信息传递的过程, 将信息从一个节点通过边传递到另一个节点.
$$
h_v^{(k)}=U_k(h_v^{(k-1)}, \sum_{u\in N(v)}M_k(h_v^{(k-1)}, h_u^{(k-1)}, x_{vu}^e))
$$

### GIN(Graph Isomorphism )

MPNN不能分别不同的图结构, 基于此GIN改进了一下.

### GAT(Graph Attention Network)

引入了Attention 在两个连接的节点

### Comparison Spectral and Spatial models

- Spectral 低效
- Spectral 需要图的傅立叶变换
- Spectral 只能用于无向图

## Pooling Modules

- 通过下采样去减少参数去生成低维的特征, 避免过拟合, 排列不变形以及计算复杂度的问题
- readout计算用于生成graph-level representation

mean/max/sum池化是比较常用的

# Graph Autoencoders

将图映射到隐空间然后再重建图结构

## Network Embedding

目标是隐空间信息.

这是一个低维的节点向量表示, 保留了节点的拓扑信息.
$$
L_1=\sum_{(v,u)\in E}A_{v,u}\Vert enc(x_v)-enc(x_u)\Vert^2\\
L_2=\sum_{v\in V}\Vert(dec(enc(x_v))-x_v)\odot b_v\Vert^2
$$

## Graph Generation

目标是生成图.

学习图的生成, 通过encode到隐空间然后再decode. 主要用于解决分子生成问题.

# Spatial-Temporal GNN

时空信息会被同时考虑.

# Application

- CV
- NLP
- Traffic
- Recommender System
- Chemistry

# Future Directions

## Model depth

深度越大效果反而不好

oversmoothing

## Scalability trade-off

通过采样, 节点可能丢失邻居信息.

## Heterogenity

当前的GNN无法直接应用到不同的图

异质图 节点不同类

## Dynamicity

考虑动态的空间关系

# 问题

- spectral
- spatial-temporal

# 研究

- GGNN(GRU GNN)
- GCN
- PGC-DGCNN
- DNGR
- GIN
- GAT







---

References

https://www.jiqizhixin.com/articles/2018-12-14-4











