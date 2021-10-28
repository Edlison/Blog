---
title: mount GDrive
categories: 
- VPS
tags: 
- linux
- ubuntu
- mount
---

# rclone

download

```sh
curl https://rclone.org/install.sh | sudo bash
```

configure

```sh
rclone config
```

follow the promt

# mount

```sh
nohup rclone mount 'remote':/remoteLoc /mnt/GoogleDrive --allow-other &> mnt_gd.out&
```

if there's an exception about `fuse`

```sh
apt install fuse
```

**the mount process need to be hang on at backgrount!**

# deamon file

[refer](https://zhujitips.com/sh/rcloned)



----

References

https://www.misterma.com/archives/900/

https://zhuanlan.zhihu.com/p/190224369

https://rclone.org