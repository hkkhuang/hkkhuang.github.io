---
title: Anaconda与ZSH不兼容问题解决
date: 2018-11-13 14:44:14
tags: [Terminal, Tools, Python]
categories: Tools
copyright: true
---

### 问题描述

需要使用pip安装一些包，打开 Anaconda Terminal后如下错误：

![](http://cdn.hkkhuang.cn/18-12-28/66536265.jpg)

<!--more-->

```
Last login: Tue Nov 13 10:52:16 on ttys001
/Users/hkkhuang/.anaconda/navigator/a.tool ; exit;
 hkkhuang@hkkhuangdeMacBook-Pro  ~   master ●  /Users/hkkhuang/.anaconda/navigator/a.tool ; exit;
/Users/hkkhuang/.anaconda/navigator/a.tool: line 1: syntax error near unexpected token `('
/Users/hkkhuang/.anaconda/navigator/a.tool: line 1: `bash --init-file <(echo "source activate /Users/hkkhuang/anaconda3;")'

[进程已完成]
```

### 问题原因

Anaconda与ZSH不兼容；

### 解决方法


在需要使用Anaconda时切换回默认终端：

```
chsh -s /bin/bash
```

重启Terminal，可以正常使用Anaconda：

![](http://cdn.hkkhuang.cn/18-12-28/69543569.jpg)

使用完成后在切换回ZSH：

```
chsh -s /bin/zsh
```


