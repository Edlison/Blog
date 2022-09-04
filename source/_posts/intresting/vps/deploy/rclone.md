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

follow the prompt

# manual

choose the binary file that match your OS

```
https://rclone.org/downloads/
```

unzip and mount to env

```sh
cp rclone /usr/bin/rclone.new
chmod 755 /usr/bin/rclone.new
chown root:root /usr/bin/rclone.new
mv /usr/bin/rclone.new /usr/bin/rclone
```

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

# bug

好像是个bug

在copy文件到OneDrive时会报错

```
2021/11/24 13:23:29 ERROR : : error listing: directory not found
2021/11/24 13:23:29 Failed to ls with 2 errors: last error was: directory not found
```

需要执行一遍

```sh
rclone ls OneDrive:
```

然后再执行`copy`指令才可以

# OD Backup script

## NextCloud

```sh
sudo /home/edlison/Applications/rclone/rclone copy /home/edlison/Applications/nextcloud OneDrive:/Cloud
```

# Vaultwarden

```sh
sudo /home/edlison/Applications/rclone/rclone copy /home/edlison/Applications/vaultwarden OneDrive:/Vaultwarden
```









----

References

https://www.misterma.com/archives/900/

https://zhuanlan.zhihu.com/p/190224369

https://rclone.org