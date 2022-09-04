---
title: Element-wise, Point-wise, Hadamard 
categories:
- Academia
tags:
- element-wise
- point-wise
---

# Intro

Element-wise, Point-wise它们的关系

<!--more-->

# Content

就是逐点或逐元素的意思.

需要做运算的两个矩阵形状完全一致, 可以是加, 减, 乘, 除运算.

```python
a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6], [7, 8]])

c = a * b
d = a.dot(b)

print('c', c)
print('d', d)
----
c [[ 5 12]
 [21 32]]
d [[19 22]
 [43 50]]
```

