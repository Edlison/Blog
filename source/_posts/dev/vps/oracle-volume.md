---
title: Attach Oracle Volume
categories: 
- VPS
tags: 
- linux
---

# Intro

将Oracle的块存储attach到VPS上

# iSCSI

>  通过TCP通信的存储设备远程映射技术

需要首先建立到块存储的连接, 参考[Oracle文档](https://docs.oracle.com/en-us/iaas/Content/Block/Tasks/attachingavolume.htm)

# 配置

1. 分区

```sh
fdisk -l  # 查看磁盘信息
fdisk /dev/sdb  # 分区
```

`n` 新建分区

`p` 新建主分区

选择开始到结束sector

`w` 写入

2. 格式化

```sh
mkfs.ext4 /dev/sdb
```

3. 挂载

   a. 临时挂载

   ```sh
   mount -t ext4 /dev/sdb /mnt/slab
   ```

   重启会失效

   b. 永久挂载

   ```sh
   vim /etc/fstab
   
   # 磁盘 挂载点 文件类型 默认项 优先级 优先级
   /dev/sdb  /mnt/slab  ext4  defaults  0  0
   ```

   ```sh
   mount -a  # 挂载生效
   ```

# 分离

关闭SCSI连接, 参考Oracle文档







----

References

https://www.jmjc.tech/less/139

https://www.cnblogs.com/zjz20/p/11237346.html
