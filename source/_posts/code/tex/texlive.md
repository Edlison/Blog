---
title: TeX Live中各程序的区别
categories:
- TeX
tags:
- latex
- pdftex
- bibtex
---

# Intro

配置VSCode中的TeX要配置编译工具和编译顺序, 这些工具的含义.

<!--more-->

# Definition

TeX: 是一种语言.
LaTeX: 是TeX中的一个集合, 与Plain TeX有这不同的格式.
pdfTeX: 是一个程序, 可以把TeX文件编译成PDF文件.
XeTeX: 是一个程序, 也可以编译TeX文件.
BibTeX: 是一个使用数据库的的方式来管理参考文献程序, 用于协调LaTeX的参考文献处理.

`pdfTeX`, `pdfLaTeX` 这两个都可以作为`pdfTeX` 的编译指令
`XeTeX`, `XeLaTeX` 这两个都可以作为`XeTeX` 的编译指令

> 使用XeLaTeX编译，如果说论文中有很图片或者其他元素没有嵌入字体的话，生成的PDF文件也会有些字体没有嵌入。
> 相反，由于PDFLaTeX使用的是TeX的标准字体，所以生成PDF时，会将所有的非TeX标准字体进行替换。
> 所以，使用PDFLaTeX生成的PDF文件默认嵌入所有字体.

# Essence

VSCode里的配置实际上就是拼命令行指令.

多次编译的问题: 中英混排, 目录索引会涉及页码、编号等，一次编译，还不能确定目录的所有信息，两次编译就会完全确定下来了，就可以输出最终结果。



----
References
https://blog.csdn.net/chen_shiqiang/article/details/52101836
https://blog.csdn.net/qysh123/article/details/11833649?utm_source=tuicool
https://www.zhihu.com/question/475204176
https://blog.csdn.net/huitailangyz/article/details/99685683