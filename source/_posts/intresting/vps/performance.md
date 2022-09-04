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

# Zench--

```sh
wget -N --no-check-certificate https://raw.githubusercontent.com/FunctionClub/ZBench/master/ZBench-CN.sh
sudo bash ZBench-CN.sh
```

# Superspeed--

```sh
wget https://raw.githubusercontent.com/oooldking/script/master/superspeed.sh
chmod +x superspeed.sh
sudo ./superspeed.sh
```

# 流媒体测试

```sh
bash <(curl -L -s https://raw.githubusercontent.com/lmc999/RegionRestrictionCheck/main/check.sh)
```

# 回程测试

```sh
wget -qO- git.io/besttrace | bash
```

```sh
wget https://raw.githubusercontent.com/nanqinlang-script/testrace/master/testrace.sh
bash testrace.sh
```

# 性能

```sh
curl -sL yabs.sh | bash
```

```sh
wget -qO- bench.sh | bash

wget -qO- git.io/superbench.sh | bash

bash <(curl -Lso- https://git.io/superspeed)
```

```sh
wget --no-check-certificate https://github.com/teddysun/across/raw/master/unixbench.sh
chmod +x unixbench.sh
./unixbench.sh
```

UnixBench时间很长





----

Reference

https://blog.zeruns.tech/archives/533.html

https://www.pigji.com/399.html