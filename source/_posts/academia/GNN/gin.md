---
title: Paper | How Powerful are Graph Neural Networks
categories:
- Academia
tags:
- GNN
---

# Intro

新的Graph Networks基本上都是基于实验直觉, 启发式探索以及反复试验得来的. 基本上没有理论的解释对于GNN.

我们提出了理论的框架起分析GNN的表示能力. GIN受到了GNN的近距离连接和Weisfeiler-Lehman(WL) test的影响.

WL test就是迭代的更新一个给定节点的特征通过不断聚合相邻节点的特征. WL test的关键在于injective aggregation 它将不同邻居节点映射到不同特征向量. (就是这个映射函数f是单射的)

我们的框架首先表示了给定节点邻居的特征向量的集合作为_multiset_, GNN内的邻居聚合可以被想成在_multiset_之上的聚合函数. 因此, 表示能力越强, GNN可以把不同的_multiset_聚合到不同的表示.

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20220124200308.png)

<!--more-->

# Preliminaries

节点v更新分为两步, aggregate和combine
$$
a_v^{(k)} = AGGREGATE^{(k)}(\{h_u^{(k-1)}:u\in N(v\})
$$

$$
h_v^{(k)}=COMBINE^{(k)}(h_v^{(k-1)}, a_v^{(k)})
$$

Aggregate把所有邻居节点的信息聚合

Combine把聚合的信息加到当前节点上, 作为更新的信息

k是迭代的步数, **是1阶邻居迭代k次**



对于节点分类问题, 节点的最后一层hv可以用来分类. 对于图分类, 再通过一个Readout function可以获得图的表示hG
$$
h_G=READOUT(\{h_v^{(K)}|v\in G\})
$$
Readout可以是简单的求和也可以是复杂的图上的pooling.

# Theoretical Framework: Overview

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20220124193317.png)

邻居节点集合的特征向量构成了`multiset`, 相同的元素可以出现多次, 因为不同的节点可以有相同的特征向量.

比如节点i和节点j都有且仅有E,F,G三个邻居节点, 那么他们通过网络映射出来的表示应该是相同的.

比如节点i有邻居节点(2, 2, 2), 节点j有邻居节点(1, 2, 3), 如果都通过(1, 1, 1)这样一个映射函数那么得到的表示是相同的, 说明这个映射不是一个单射函数, 也就不是powerful的GNN.

最powerful的GNN不会映射两个不同的邻居节点集合(multisets), 到一个相同的表示. 聚合函数是单射的.

# Graph Isomorphism Network

我们想让同构图被映射到相同的表示, 非同构图被映射到不同的表示.

如果邻居聚合和图上的readout function都是单射的, GNN的结果就和WL test一样powerful.

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20220124195723.png)

满足定理3的就是powerful GNN, 不满足的就是less powerful GNN.

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20220124195859.png)

GIN更新节点





























