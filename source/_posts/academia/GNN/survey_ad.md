---
title: A Comprehensive Survey on Graph Anomaly Detection
categories:
- Academia
tags:
- GNN
- survey
- Anomaly Detection
---

# Intro



# Challenges

## Anomaly-aware training objectives

在判断异常数据, 及设计Loss比较困难

## Anomaly interpretability

异常检测的可解释性

## High training cost

图包含的信息更多, 需要消耗更多时间与空间资源

## Hyperparameter tuning

超参数调优, 特别是在非监督学习下, 通过没有打过标签的数据很难判断模型的性能.

# Preliminaries

## Plain Graph

静态的图结构
$$
G={V,E}
$$

$$
V={v_i}^n,
E=\{e_{i,j}\}
$$

$$
A=[a_{i,j}]_{n*n}
$$

邻接矩阵存储结构信息

## Attributed Graph

$$
G=\{V,E,X\}
$$

$$
X=[x_i]_{n*k}
$$

X是节点上的特征向量, k维

## Dynamic Graph

$$
G(t)=\{V(t), E(t), X_v(t), X_e(t)\}
$$

代表t时刻图的结构, $X_v$是node的特征向量, $X_e$是edge的特征向量.

# Anomalous Node Detection

**Global anomalies**

只考虑节点特征, 完全不同于其他节点的.

**Structural anomalies**

只考虑图结构信息, 有着不同连接模式的节点是异常节点.

**Community anomalies**

同时考虑节点属性和图结构信息, 在一个区域内与其他节点有着不同的特征.

例

![](https://i.imgur.com/V1N6ugS.png)

Node14是Global异常, 它有别于所有其他节点特征.

Node5,6,11是Structural异常, 它们的结构信息与内部的其他节点不一样.

Node2, 7是Community异常, 它有别于内部的其他节点特征.

## on Plain Graphs

### Non-Deep Learning

使用统计特征, 如in/out的度数.

### Deep Learning

深度学习的方法将图结构encode到一个embedding向量, 然后在对异常节点进行进一步分析.

检测结构异常
1. 分割算法: node到d个communities
2. 使用一个embedding算法, 拿到节点link信息的embedding
3. 如果node属于community-c,yc的值就高.
4. 计算nodei到所有邻居节点的分数, 如果有link到community那么分数就高.
5. Score把这些分数加起来, 如果link到了多个community异常分数就会很高.

## on Attribute Graphs

### AutoEncoder Based

DONE这个无监督的方法计算异常值, Attribute和Structure两个AutoEncoder

1. 与不同community的nodes有相似的属性. o^a
2. 与其他community相连接. o^s
3. 结构上属于一个community但是属性和其他的community相似. o^com

设计了5个Loss函数

1. 2个重建Loss函数

![](https://i.imgur.com/GONRj6h.png)

2. 2个同质Loss函数

![](https://i.imgur.com/bJH72RF.png)

![](https://i.imgur.com/ltUrNBh.png)

3. 结构异常与属性异常的互补Loss函数

![](https://i.imgur.com/q9cMLHx.png)

不可能同时是attribute异常和community异常吗?

- 前面的loss可以判断

### GCN based

- DOMINANT 方法

### Reinforcement Learning Based

- GraphUCB 方法

### GAT based





























