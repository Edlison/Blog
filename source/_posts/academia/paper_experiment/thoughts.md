---
title: ClusterGAN训练的一些思考
categories:
- Paper
---

GAN太难训练，经常遇到先收敛后发散的情况。

# 数据集

数据类别不平衡的问题可能会导致encoder效果不佳的状况



# 预处理

注意分**连续数据**与**离散数据**。

连续数据注意**归一化**

离散数据处理成**one_hot**

图像一定要归一化！！！



# 网络设计

归一化后的数据要与选择的**激活函数相对应**

离散数据最后一层改成**softmax**



# 训练

Discriminator可以设定clamp防止训练发散



# 超参数

batch_size 大概能将整个数据集分成20个iter左右

beta 对于联合loss训练的注意设置倍数 来**弱化或增强**某个loss组成



# Tips

查看效果的时候注意记录各个参数下的结果

