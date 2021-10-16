---
title: sh of testing performance on VPS
categories: 
- VPS
tags: 
- sh
- linux
---

# Superbench

```sh
wget -N --no-check-certificate https://raw.githubusercontent.com/oooldking/script/master/superbench.sh
sudo bash superbench.sh
# or
curl -Lso- https://raw.githubusercontent.com/oooldking/script/master/superbench.sh | bash
```

# Lemonbench

```sh
curl -fsL https://ilemonra.in/LemonBenchIntl | bash -s fast
curl -fsL https://ilemonra.in/LemonBenchIntl | bash -s full
```

# Zench

```sh
wget -N --no-check-certificate https://raw.githubusercontent.com/FunctionClub/ZBench/master/ZBench-CN.sh
sudo bash ZBench-CN.sh
```

# Superspeed

```sh
wget https://raw.githubusercontent.com/oooldking/script/master/superspeed.sh
chmod +x superspeed.sh
sudo ./superspeed.sh
```





----

Reference

https://blog.zeruns.tech/archives/533.html