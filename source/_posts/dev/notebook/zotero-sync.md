---
title: Zotero File Sync
categories:
- Notebooks
tags:
- zotero
---

# Intro

Zotero文件同步的一些问题

<!--more-->

# Sync

Zotero的文件分为2部分`Data`与`File`

## Data

`Data`部分包括所有文件, 除了attachment.

仅可以通过Zotero官方进行存储, 且没有容量限制.

因此必须登录Zotero账号才能同步数据.

## File

`File`部分包括所有的attachment.

这一部分可以通过3种方式同步

- Zotero Storage
- WebDAV
- Linked File Attachments

# Plan

多设备上同步的终极解决方案

- Data部分通过Zotero同步

- File部分通过WebDAV同步

- ZotFile同步到移动端设备

## Tablet

在ZotFile配置文件中打开`Use ZotFile to send and get files from tablet`

选择iCloud中MarginNote文件夹作为同步目录

右键想要同步的文件`send to tablet` 

移动端编辑完成后在`Tablet Files (modified)`文件夹中右键取回`get from tablet` 

# Error

## 上传时报错

```
Your WebDAV server returned an HTTP 413 error for a PUT request.
```

这是由于使用了反代服务器, nginx默认客户端上传文件单个<1M.

有一个文件达到了15M, 所以上传不了.

在nginx http段中加入

```nginx
client_max_body_size 30M;
client_body_buffer_size 2M;
```

## 分两次上传没有验证文件存在

一开始因为nginx的原因>1M的文件没有同步, 修改好后把WebDAV上的同步文件删除了, 结果只同步了>1M的文件.

把File同步设置为Zotero->WebDAV删掉文件夹->File同步改回来.







---

References

https://www.zotero.org/support/sync

http://zotfile.com/index.html

https://blog.csdn.net/u012814506/article/details/47761429