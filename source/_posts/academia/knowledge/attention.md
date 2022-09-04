---
title: Attention 新理解
categories:
- Academia
tags:
- Attention
---

# Intro

对Attention的一些新的理解

<!--more-->

# Taxonomy

Attention机制本质上就是加权, 不同的Attention也就是采用了不同的加权机制.

1. Self-Attention(Seq2Seq)

Self-Attention就是Tranformer中提出来的, 这里的注意力同时关注了输入和输出, 因此称为**Self** Attention. 这种注意力机制主要用于解决Seq2Seq问题, 比如机器翻译, 问答系统.

2. RNN-Attention(NLP)

RNN注意力, 用在RNN这种结构上, 主要是解决一些NLP的问题, 比如classification. (这里更强调是应用在RNN上, 对NLP的分类并不准确.)

3. CNN-Attention(CV)

CNN注意力, 用在CNN这种网络结构上. 主要解决一些CV问题.

# Methods

获取注意力机制主要的方法.

## 增强特征聚合

比如在Transformer中, input特征与output特征相聚合

比如在GAT中, 

## 通道与空间注意力相结合

比如在Convolutional Block Attention Module中, 即考虑了通道域又考虑到了空间域.





---

References

https://blog.csdn.net/ZXF_1991/article/details/104615942

https://www.cnblogs.com/bupt213/p/10826093.html