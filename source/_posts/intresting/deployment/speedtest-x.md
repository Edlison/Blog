---
title: speedtest-x via docker
categories: 
- VPS
tags: 
- docker
---

# Intro

speedtest-x

<!--more-->

# Compose

```yaml
version: '3.3'

services:
  speedtest-x:
    image: badapple9/speedtest-x
		ports:
		  - 9999:80
```

