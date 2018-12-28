---
title: Python3学习记录【001】---在不同操作系统中搭建 Python 编程环境
date: 2018-04-25 18:46:52
tags: [Python, Windows, Linux]
categories: Python
copyright: true
---

开始接触Python，想要在学习的过程中记录一下自己的学习过程。
开始学习前首先把需要的环境配置一下吧！
### 在 Windows 系统中搭建 Python 编程环境
1、 Windows系统没有默认安装了Python，需要下载并安装，根据系统版本下载Python安装包。
<!-- more -->
**[下载地址：https://www.python.org/downloads/](https://www.python.org/downloads/)**

![](http://cdn.hkkhuang.cn/18-12-28/79456651.jpg)
2、下载安装程序后，双击下载好的安装文件进行安装。

![](http://cdn.hkkhuang.cn/18-12-28/73053867.jpg)

**注意：请务必选中复选框` Add Python to PATH` ，这样能够方便之后的配置。**
默认安装：
![](http://cdn.hkkhuang.cn/18-12-28/90082237.jpg)
安装成功：

![](http://cdn.hkkhuang.cn/18-12-28/40265745.jpg)

![](http://cdn.hkkhuang.cn/18-12-28/21554001.jpg)
            
3、 安装完成后，验证是否正确安装。可以通过Python自带的IDLE和终端窗口开始使用Python，也可以使用Win+R组合键，输入cmd打开命令提示符窗口，再输入python进入交互式终端。
输出一条“Hello World hkkhuang” 信息检验一下，环境配置成功。

![](http://cdn.hkkhuang.cn/18-12-28/51178465.jpg)

![](http://cdn.hkkhuang.cn/18-12-28/99911618.jpg)

### 安装IDE 选择PyCharm
PyCharm 可以跨平台!

**[下载地址：https://www.jetbrains.com/pycharm/download/#section=windows](https://www.jetbrains.com/pycharm/download/#section=windows)**

选择Community版本（免费使用）

![](http://cdn.hkkhuang.cn/18-12-28/66201924.jpg)

安装详细过程不再赘述。

### 在 Linux 系统 Ubuntu 中搭建 Python 编程环境
1、一般的Linux系统中都带有Python2.7,我们现在升级为3.x,这是之前配置留下记录（Python版本为3.4）
安装Python3.4，使用命令：

```
sudo apt-get install python3.4
```

![](http://cdn.hkkhuang.cn/18-12-28/55810658.jpg)

2、因为Python3和python2并不兼容，所以要删除python2的默认python link文件，使用命令：

```
	sudo rm /usr/bin/python
```

3、删除python2的默认python link文件后将Python3的link文件在原来位置创建，使用命令：
```
sudo ln -s /usr/bin/python3.4 /usr/bin/python
```

4、验证python的版本，成功升级到Python3.4
```
python
```

![](http://cdn.hkkhuang.cn/18-12-28/85963098.jpg)
