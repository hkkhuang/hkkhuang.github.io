---
title: dpkg命令
date: 2018-10-17 14:26:49
tags: [Tools, Linux]
categories: Linux
copyright: true
---

# dpkg命令

dpkg命令是Debian Linux系统用来安装、创建和管理软件包的实用工具。

## 语法
```
dpkg(选项)(参数)
```

## 选项

```
-i：安装软件包；
-r：删除软件包；
-P：删除软件包的同时删除其配置文件；
-L：显示于软件包关联的文件；
-l：显示已安装软件包列表；
--unpack：解开软件包；
-c：显示软件包内文件列表；
--confiugre：配置软件包。

```
<!--more-->

## 参数

```
Deb软件包：指定要操作的.deb软件包。
```

## 实例
```
dpkg -i package.deb     #安装包
dpkg -r package         #删除包
dpkg -P package         #删除包（包括配置文件）
dpkg -L package         #列出与该包关联的文件
dpkg -l package         #显示该包的版本
dpkg --unpack package.deb  #解开deb包的内容
dpkg -S keyword            #搜索所属的包内容
dpkg -l                    #列出当前已安装的包
dpkg -c package.deb        #列出deb包的内容
dpkg --configure package   #配置包
```

参考：

[Linux命令大全：http://man.linuxde.net/dpkg](http://man.linuxde.net/dpkg)