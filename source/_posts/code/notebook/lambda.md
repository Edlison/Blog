---
title: Python中的Lambda
categories:
- Development
tags:
- Python
---

# Intro

Python中lambda的使用

<!--more-->

# Content

语法:

lambda arguments: expression

返回的是一个函数, 函数的参数由arguments来声明, expression是函数的表达式.

如果lambda的参数和外层参数的命名一样了, 则互不影响.

如果不一样, 外部的参数可以直接参与到lambda函数内的计算.

例子:

```python
def test1(x):
  return lambda a, b: x + x + a + b

# test(10)(1, 3) = 24

def test2(x):
  return lambda x: x + x + x

# test(100)(1) = 3
```



----

Reference

https://www.w3school.com.cn/python/python_lambda.asp