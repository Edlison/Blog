---
title: Home Lab | Virtualization
categories:
- Home Lab
tags:
- pve
---

# Intro

使用虚拟化技术搭建Home Lab

# Process

## PE(preinstallation environment)

使用U盘制作一个PE盘, 方便将主机格式化, 新建分区.

系统崩了可以通过PE恢复.

1. 下载[wepe](http://wepe.com.cn)
2. 选择U盘进行安装
3. 三个分区: PE系统分区(看不见), UEFI引导分区, 剩余分区(放iso)

## PVE bootloader

1. 下载[PVE](https://proxmox.com/en/)
2. 下载[refus](http://rufus.ie/)
3. 使用refus 将PVE镜像写入U盘

## install PVE

按照指引安装

CIDR自己设置, 需要和router在一个网络号下

通过设置的地址访问

## iommu

设置iommu分组与硬件直通

**BIOS开启VT-d(不在cpu控制里)**

### 对于grub引导

```sh
# vi /etc/default/grub

GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on pcie_acs_override=downstream,multifunction"
```

需要添加`pcie_acs_override=downstream,multifunction`将同一个网卡设备上的多个接口进行分组

```sh
update-grub
```

### 对于systemd-boot引导

```sh
# vi /etc/kernel/cmdline

quiet intel_iommu=on pcie_acs_override=downstream,multifunction
```

直接创建文件, 添加指令

```
proxmox-boot-tool refresh
```

### 修改modules文件

```sh
# vi /etc/modules

vfio
vfio_iommu_type1
vfio_pci
vfio_virqfd
```

```sh
update-initramfs -u -k all
```

### 检查效果

```sh
dmesg | grep -e DMAR -e IOMMU
find /sys/kernel/iommu_groups/ -type l
```

# 注意

PVE中有两个默认的storage

local: 放镜像文件, 可用于虚拟机的系统镜像, 共58G

local-vm: 虚拟机的磁盘大小, **也可以通过指令挂载, 然后设置为引导程序**, 共151G

*PVE装在240G硬盘中







---

Reference

https://post.smzdm.com/p/alpwlzvp/

https://pve.proxmox.com/wiki/Pci_passthrough#systemd-boot
