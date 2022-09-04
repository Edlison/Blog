---
title: xxx is a zip archieve (do you mean torch.jit.load)
categories:
- Error
tags:
- pytorch
---

# Intro

在加载torch保存的模型时报错

`xxx is a zip archieve (do you mean torch.jit.load)`

<!--more-->

# 原因

由于torch1.6后采用zip存储权重文件, 与之前版本不兼容

# 解决

```python
torch.save(file, target, _use_new_zipfile_serialization=False)
```







----

Reference

https://blog.csdn.net/irober/article/details/115144522