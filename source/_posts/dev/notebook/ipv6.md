---
title: IPv6 VPS
categories:
- Notebooks
tags:
- ipv6
---

# Intro

初始化IPv6的机器

<!--more-->

# Login

```sh
ssh root@2a02:0180:0006:0001:0000:0000:0000:1e48
scp id_rsa_common.pub root@\[2a02:0180:0006:0001:0000:0000:0000:1e48\]:~/
```

注意: `zsh` 需要对`[]` 进行转义.

使用`ping6` 指令

```sh
ping6 2a02:0180:0006:0001:0000:0000:0000:1e48
```

