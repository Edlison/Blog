---
title: TeX 公式
categories:
- TeX
tags:
- math
---

# Intro

LaTeX公式语法

<!--more-->

# Main

> https://zhuanlan.zhihu.com/p/110756681

## 加粗

```latex
\textbf{xxx}
\mathbf{xxx}
\pmb{\theta}

```

## 波浪线

```latex
说明：由于latex中 ~ 按键有特殊用途，因此需要用其他方式才能打出 ~

方式1：一般文字环境下，\textasciitilde
方式2：公式环境下，$ \sim $
```

## 大写空心

```latex
需要添加宏包 \usepackage{amsfonts}

A \mathbb{A}A ： \mathbb{A}
B \mathbb{B}B ： \mathbb{B}
C \mathbb{C}C ： \mathbb{C}
```

## 下标显示在正下方

```latex
\mathop{\mathbb{E}}\limits_{x\sim pX(x)}

\mathop{\mathbb{E}}_{x\sim pX(x)}
```

注意: 

- \limits操作需要被添加角标的表达式为数学符号

- \mathop将表达式变为数学符号

## 范数

```latex
L1
$\Vert x \Vert_1$
L2
$\Vert x \Vert_2$
无穷
$\Vert x \Vert_\infty$
```

## 换行

```latex
\begin{equation}
\begin{aligned}
......
\end{aligned}
\end{equation} 
```

注意:

报错`Misplaced alignment tab character &.` 需要导包 `\usepackage{amsmath}`

## 花体

**mathbb**

常用作数域的表示,比如实数域,复数域等.

```
包名 amssymb
用法 \mathbb{}
```

**mathscr**

常用作空间或者变换的表示.

```
包名 mathrsfs
用法 \mathscr{}
```

**mathcal**

泛函分析中所有线性算子的集合

```
包名 amssymb
用法 \mathcal{}
```

**mathfrak**

紧算子的全体用到了这个字体.

```
包名 amssymb
用法 \mathfrak{}
```

## 空格

```latex
两个quad空格 两个m的宽度
a \qquad b
quad空格	一个m的宽度
a \quad b
大空格 1/3m宽度
a\ b
中等空格 2/7m宽度
a\;b
小空格 1/6m宽度
a\,b
没有空格
ab	 
紧贴 缩进1/6m宽度
a\!b
```



















----

References

https://zhuanlan.zhihu.com/p/110756681

https://blog.csdn.net/shenquanyue/article/details/84999300

https://blog.csdn.net/qq_41688829/article/details/114778978

https://www.jianshu.com/p/5d1157f7ad88