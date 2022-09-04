---
title: sh of testing performance on VPS 2.0
categories: 
- VPS
tags: 
- sh
- linux
---

# Intro

常用测试脚本2.0

<!--more-->

# yabs

硬件信息+IO+测速+跑分

```sh
curl -sL yabs.sh | bash
```

# speedtest

硬件信息+Geekbench

```sh
wget https://bench.monster/speedtest.sh
bash speedtest.sh -gb5
```

# Bench

硬件信息+IO+测速

```sh
wget -qO- bench.sh | bash
```

# 国内测速

下载上传延迟测速

speedtest

```sh
bash <(curl -Lso- http://yun.789888.xyz/speedtest.sh)
```

superspeed

```sh
bash <(curl -Lso- https://git.io/superspeed.sh)
```

# 回程路由测试

三网回程路由

```sh
wget -qO- git.io/besttrace | bash
```

# 流媒体解锁测试

```sh
bash <(curl -L -s https://raw.githubusercontent.com/lmc999/RegionRestrictionCheck/main/check.sh)
```

