---
title: TeX Syntax
categories:
- TeX
---

# Intro

TeX的语法

<!--more-->

# Basic

```tex
\documentclass{article}
\usepackage{a4}

\title{Hello World}
\author{Edlison}
\date{\today}

\begin{document}
\maketitle

\tableofcontents

\part{part title}
\section{section title}
\subsection{subsection title}
\subsubsection{subsubsection title}
\paragraph{paragraph title}
\subparagraph{subparagraph title}



\input{intro.tex}

\input{experiment.tex}

\end{document}
```

`input` 插入`.tex` 文件就相当于是拼接内容.

# Package

如果要自行下载包文件, 安装到

`/usr/local/texlive/2019/texmf-dist/tex/latex`

目录下.