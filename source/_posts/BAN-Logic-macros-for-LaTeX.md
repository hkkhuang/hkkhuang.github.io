---
title: BAN Logic macros for LaTeX
date: 2019-02-25 19:59:40
tags: [Latex, Tools]
categories: Tools
copyright: true
---

### BAN Logic macros for LaTeX

一个用于向Latex文档添加BAN Logic符号的宏列表。

Commands are named as symbol names (like \sees, \believs, and so on).

命令被命名为符号名称（如\see，\believs等）。

<!--more-->

```
% Packages
\usepackage{mathtools}
\usepackage{amssymb}

% Macros
\newcommand{\believes}{\mid\equiv}
\newcommand{\sees}{\triangleleft}
\newcommand{\oncesaid}{\mid\sim}
\newcommand{\controls}{\Rightarrow}
\newcommand{\fresh}[1]{\#(#1)}
\newcommand{\combine}[2]{{\langle #1 \rangle}_{#2}}
\newcommand{\encrypt}[2]{{ \{ #1 \} }_{#2}}
\newcommand{\sharekey}[1]{\xleftrightarrow{#1}}
\newcommand{\pubkey}[1]{\xmapsto{#1}}
\newcommand{\secret}[1]{\xleftrightharpoons{#1}}

% Examples
\[A \believes B \]
\[A \sees B \]
\[A \oncesaid B \]
\[A \controls B \]
\[\fresh{X} \]
\[\combine{X}{Y} \]
\[\encrypt{X}{Y} \]
\[A \sharekey{k} B \]
\[\pubkey{k} B \]
\[A \secret{k} B \]
```

效果如下：

![](http://cdn.hkkhuang.cn/20190225195726.png)


> [http://www.lecaldare.com/ban-logic-macros-for-latex/](http://www.lecaldare.com/ban-logic-macros-for-latex/)

> [https://github.com/psoftware](https://github.com/psoftware)
