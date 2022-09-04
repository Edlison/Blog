---
title: Home Lab prerequisite
categories:
- Home Lab
---

# Intro

开始搭建Home Lab的前期准备工作

# 预备知识

## Legacy - UEFI

Legacy这种启动模式兼容性较好，在安装操作系统时只可以选择32位或64位的，但是硬盘分区最大支持支持2TB，理论支持安装Windows所有版本的系统；而UEFI启动模式只能安装64位的操作系统，硬盘分区最大支持18EB，基本上算是无限大，相对启动速度会更快，同时为用户在BIOS中提供支持鼠标等功能的更高级的图形界面。

## DHCP

Dynamic Host Configuration Protocol(动态主机配置协议)

C/S形式, 客户端向服务端申请IP, 服务端动态生成IP并分发

AP(access point)桥接模式下需要关闭DHCP

## PCI PCIe

Peripheral Component Interconnect Express

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20211029230958.png)

带宽的计算公式
$$
带宽=时钟*(位宽/8)
$$
PCIe尺寸

- 半长<167.65mm
- 全长<312.00mm
- 半高<68.9mm
- 全高<111.15mm

一些服务器上的PCIe设备需要通过转接器才能装在主机上.

由于适配问题x4, x8, x16都是一样大的

x1也可以装在x16上, 且占用的只是x1的带宽

## 南桥北桥

> 其中的北桥负责CPU与内存的数据交换、图形处理、CPU与PCIE数据交换; 南桥则负责系统的输入输出功能。
>
> 所以北桥芯片还有个名字叫“图形与内存控制器”，南桥叫“输入/输出控制器”。

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20211029232104.png)

与CPU直接相连的PCIe3.0一共就16位, 上限16GB/s

而从南桥过来的所有数据共享一个DMI3.0总线, 实际上是PCIeX4, 因此上限为4GB/s

m.2走南桥PCIe通道, 最快也就4GB/s

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20211030001812.png)

## 接口

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20211030002007.png)

### m.2

是一种接口, 有多种长度可选

最普通的m.2走SATA通道, m.2 NVMe走PCIe通道

以上两种不兼容, SATA协议有3段金手指, NVMe协议有两段金手指

### NVMe

是一种协议, PCIe是一种通道, NVMe协议基于这个通道上实现了性能增强, 延迟降低



## iperf

测试带宽性能

## 多播

> https://zhuanlan.zhihu.com/p/42431093

## SR-IOV

Single Root I/O Virtualization

对PCIe接口IO硬件进行虚拟, 需要软件硬件同时支持

### 常见设备

hp331flr - Broadcom bcm5419 不支持 1Gbps*4

hp366flr - Intel i350T4 支持 1Gbps*4

hp561flr - Intel x540T2 支持 10Gbps*2

## raid

> https://zhuanlan.zhihu.com/p/119452913

## 硬盘

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20211030003204.png)



## 网线

千兆

1000Mbps - 1Gbps - 125MBps

万兆

10000Mbps - 10Gbps - 1.25GBps

CAT5(5类线)

100Mbps

CAT5e(超5类线)

1000Mbps

CAT6(6类线)

1Gbps

CAT6e(超6类线)

10Gbps







----

Reference

https://zhuanlan.zhihu.com/p/26172972

https://zhuanlan.zhihu.com/p/375804757

https://post.smzdm.com/p/aoow85z7/

https://zhuanlan.zhihu.com/p/42431093

https://zhuanlan.zhihu.com/p/119452913
