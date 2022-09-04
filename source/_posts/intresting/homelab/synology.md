---
title: Home Lab | Synology
categories:
- Home Lab
tags:
- synology
---

# Intro

群晖NAS系统

# Process

1. 新建虚拟机4C4G
2. 分配的硬盘可以随便设置
3. 将硬盘分离并删除
4. 使用`img2kvm`工具把synology引导文件转换为虚拟机的磁盘镜像

```sh
./img2kvm synboot.img 103 vm-103-disk-0
```

5. **在PVE中会显示这个vm-103-disk-0, 将它以sata添加到虚拟机**
6. `ls -l /dev/disk/by-id`查看硬盘信息
7. 将硬盘直通到虚拟机

```sh
qm set 103 --sata1 /dev/disk/by-id/ata-WDC_WD10EZEX-00BN5A0_WD-WCC3F3504336
```

8. 在PVE中会显示已经自动挂载
9. [find synology](http://find.synology.com)查找局域网内的群晖设备

# 问题

## 两个硬盘

群晖的HDD中一块硬盘一直显示有两个硬盘

![](https://blogimg-1304875656.cos.ap-hongkong.myqcloud.com//20211029222625.png)

因为这里显示的硬盘1是52MB, 又因为引导固件也是52MB, 所以怀疑是在添加固件的时候固件被放到了这个硬盘中?

重新装了很多遍, 包括格式化硬盘重新分区, 还是有这个问题.

## 7.x版本

6.23版本引导固件正常使用, 需要在官网下载6.23版本DSM

7.0.1版本引导固件无法正常引导. 好像需要改成UEFI引导方式以及其他...







---

Reference

https://post.smzdm.com/p/alpwlzvp/

http://www.nasyun.com/thread-77818-1-1.html