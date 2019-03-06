---
title: >-
  Mac启动MySQL失败，报错信息：Warning:The /usr/local/mysql/data directory is not owned by
  the 'mysql' or '_mysql' user
date: 2019-03-06 21:01:31
tags: [MySQL, Tools]
categories: Tools
copyright: true
---

Mac启动MySQL失败，报错信息：Warning:The /usr/local/mysql/data directory is not owned by the 'mysql' or '_mysql' user

### 问题描述
Mac在ＭySQL启动或开机自动运行时，报错，如下图

在ＭySQL操作面板上会提示“Warning:The /usr/local/mysql/data directory is not owned by the 'mysql' or '_mysql'”
![](http://cdn.hkkhuang.cn/20190306203421.png)

<!--more-->
### 分析原因

Mac OS X的升级或其他原因可能会导致ＭySQL启动或开机自动运行时出错。

### 解决方法

应该是某种情况下导致/usr/local/mysql/data的宿主发生了改变

mac 下面运行 “`sudo chown -R_mysql:wheel/usr/local/mysql/data`”

即可正常启动：

![](http://cdn.hkkhuang.cn/20190306205411.png)



> [https://stackoverflow.com/questions/5527676/warning-the-user-local-mysql-data-directory-is-not-owned-by-the-mysql-user](https://stackoverflow.com/questions/5527676/warning-the-user-local-mysql-data-directory-is-not-owned-by-the-mysql-user)
> [https://blog.csdn.net/lvsijian8/article/details/60779386](https://blog.csdn.net/lvsijian8/article/details/60779386)