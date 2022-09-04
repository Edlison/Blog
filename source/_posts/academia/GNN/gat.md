---
title: Paper | Graph Attention Networks
categories:
- Academia
tags:
- attention
- GNN
---

# Intro

精读Graph Attention Networks 论文

<!--more-->

# GAT Architecture

网络输入node集合的feature h, 输出h'
$$
h=\{h_1, h_2, ..., h_N\}
$$

$$
h'=\{h_1', h_2', ..., h_N'\}
$$

节点j对节点i的相关系数
$$
e_{ij}=a(Wh_i,Wh_j)
$$
代表着节点j的特征对于节点i的重要性

其中W是一个线性变化的权重矩阵, 并且同时应用在i和j节点.

其中a是注意力机制, 也是共享在每一个节点.

对e展开
$$
e_{ij} = LeakyReLU(\overrightarrow{a^T}[W\overrightarrow{h_i}\Vert W\overrightarrow{h_j}])
$$
||是拼接

然后对节点i的所有邻居节点j进行归一化
$$
\alpha_{ij}=softmax_j(e_{ij})
$$
拿到了归一化后的注意力相关性信息就可以应用在获取节点i的所有特征了.

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20220119200029.png)

计算节点i的alpha

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20220119200038.png)

引入多头注意力机制

注意力后的特征
$$
\overrightarrow h_j' = \sigma(\sum_{j\in{N_i}}\alpha_{ij}W\overrightarrow h_j)
$$

$$
\overrightarrow h_j' = \Vert_{k=1}^K \sigma(\sum_{j\in{N_i}}\alpha_{ij}^kW^k\overrightarrow h_j)
$$

如果是在最后一层, 多头注意力就不能简单的拼接起来了, 要使用一个平均, 最后再来一个归一化.
$$
\overrightarrow h_j' = \sigma({1\over K}\sum_{k=1}^K\sum_{j\in{N_i}}\alpha_{ij}^kW^k\overrightarrow h_j)
$$


通过mask来注入图的结构

---

Reference

Veličković, Petar, et al. "Graph attention networks." *arXiv preprint arXiv:1710.10903* (2017).
