---
title: Home Lab | Win10
categories:
- Home Lab
tags:
- win10
---

# Intro

在PVE虚拟机上安装Win10

<!--more-->

# Preperation

[下载Win10镜像](https://next.itellyou.cn/Original/Index)

[下载Virtio驱动](https://docs.fedoraproject.org/en-US/quick-docs/creating-windows-virtual-machines-using-virtio-drivers/index.html)



# Installation

虚拟机创建好后再创建一个CD驱动器, 选择Virtio驱动



# 显卡直通

## grub文件

```
GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on video=efifb:off"
```

````sh
update-grub
````



## blacklist

```
blacklist nvidiafb
blacklist radeon
blacklist nvidia
blacklist amdgpu
blacklist snd_hda_intel
blacklist snd_hda_codec_hdmi
blacklist i915
```

```sh
update-initramfs -u
```

## 绑定到vfio模块

查看显示和音频设备

```sh
lspci -n | grep -E "0300|0403"
```

添加到vfio

```sh
echo "options vfio-pci ids=10de:1187,8086:8c20" > /etc/modprobe.d/vfio.conf
```

添加options防止VM死机

```sh
echo "options kvm ignore_msrs=1" > /etc/modprobe.d/kvm.conf
```

更新配置 重启

```sh
update-initramfs -u
reboot
```

查看是否正常加载

```sh
lsmod | grep vfio
```

# 问题

只要添加PCIE设备PVE就会卡死







---

References

https://www.simaek.com/archives/69/

https://www.10bests.com/win10-htpc-on-pve/









