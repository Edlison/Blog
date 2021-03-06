---
title: 区块链技术
catagories:
- BlockChain
---

# 对区块链技术新的理解

底层技术目前都是一样的，通过chain将block连起来，通过代码确定**共识机制**，采取分布式的策略达到不可篡改性。

目前感觉技术上有很大不同的是有两个代表。**比特币**与**以太坊**。

# 比特币与以太坊对比

## 比特币

### 交易

比特币的职能只有一个，**传递价值并存储价值**。

其交易过程为：

- TO: 发给谁
- FROM: 谁发送的
- AMOUNT: 发送的数量

## 以太坊

### 交易

以太坊最大的不同在于它在交易的时候还有一个`DATA`字段。

1. 传递价值（与比特币相同）
- - TO: 发送给谁
  - FROM: 谁发送的
  - AMOUNT: 发送的数量
2. 创建合约
- - TO: nil(空白为触发创建智能合约)
  - FROM: 谁创建的
  - AMOUNT: 可以是0或是任意数量的以太币，它是我们想要给合约的存款。
  - DATA: 包含编译为字节码的智能合约代码
3. 调用合约函数
- - TO: 目标合约账户地址
  - FROM: 谁调用的
  - AMOUNT: 可以是零或是任意数量的以太币，例如**可以支付合约服务费用**。
  - DATA: 包含函数名和参数（标识如何调用智能合约函数）

**理解**：每次进行代币（Token）交易的时候都会**对合约进行请求**，比如交易时的费用等。

**问题**：超发，被盗等操作如何实现？

### 智能合约

由于ETH最大的区别在于可以传`DATA`, 因此**衍生出来了一个智能合约的概念**。

**其本质就是可以在区块链上运行代码。**

#### 用户账户

- 地址
- 余额

该余额就是用户的钱。

#### 合约账户

- 地址
- 余额
- 状态
- 代码

合约账户也拥有**余额**，意味着一个**实例化出来的合约对象**可以**通过代码管理余额**，如果代码有问题，则会产生错误。

合约账户的**状态**是只能合约中生声明的所有变量和变量的当前状态，**就如同实例化的一个对象中的变量**。这个对象将永远存在区块链网络中，除非程序自毁。

合约账户的**代码**是编译后可以在客户端和节点可以运行的字节码，它在**合约创建时实例化**。

智能合约是**图灵完备**的，理论上可以做任何事情。

### GAS

在链上的操作（转账，合约的部署，合约的执行）都是需要占用资源的，这个GAS将被付给矿工。

GAS可以自己设定，出价越高被执行的就越快。

# 理解

区块存储任何东西

账户可以用**地址**表示，交易可以用**地址**表示，合约账户内的代码等都可以用**地址**表示。







----

Reference

https://learnblockchain.cn/2018/01/04/understanding-smart-contracts