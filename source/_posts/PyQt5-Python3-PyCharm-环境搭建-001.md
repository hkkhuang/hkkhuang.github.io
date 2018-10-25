---
title: 'PyQt5-Python3-PyCharm 环境搭建-001'
date: 2018-10-24 21:37:33
tags: [Tools, Python,PyQt5]
categories: Python
copyright: true
---

### 基本开发环境版本信息：

* MAC OS 10.14 版本 
* Pycharm 2016.3.2 版本 
* Python 3.6.6 版本
* PyQt5 5.11.2 版本
* pyinstaller：将python代码打包为可执行的exe文件。

### 需要安装的工具/包

* sip
* PyQt5
* Qt
* python

### sip

在从源代码构建PyQt5之前，您必须已经构建并安装了SIP，就是说你必须要安装这个东西，那么这个东西是什么呢？

#### 什么是sip？
sip是RiverBank（也就是PyQt的开发商）开发的用于PyQt的Python/C++混合编程解决方案。由于Qt框架的复杂性，PyQt并没有使用Cython、SWIG的混合编程方案，而是自己单独做了一套框架。sip包括一个sip工具、SDK和Python Module。

与SWIG类似，使用sip也需要先编写一个『配置文件』，然后使用sip工具『编译』为C++源文件，最后，和Qt库一起编译形成适用于Python的PyQt。

与SWIG不同的是，sip同时以Python Module的形式存在，也就是说，作为Python Module的PyQt，依赖于作为Python Module的sip。而对于SWIG，一旦自动生成的C++生成完毕，整个流程就不再依赖SWIG了。

#### 安装sip

##### 方式一：pip安装
使用支持的Python版本，你可以从PyPi安装SIP 通过运行：

```
pip install SIP
```

##### 方式二：使用Homebrew

```
brew install sip
```

#### 安装PyQt5

##### 方式一：pip安装
使用支持的Python版本，你可以从PyPi安装SIP 通过运行：

在Anaconda中新建一个环境，专门用于PyQt5的环境搭建：

![](http://p6dpqooos.bkt.clouddn.com/18-10-24/58641812.jpg)

在该新建的环境下，打开Terminal，使用pip方式安装PyQt5，命令如下：

```
pip install PyQt5
```

安装完成：

![](http://p6dpqooos.bkt.clouddn.com/18-10-24/51277945.jpg)


##### 方式二：使用Homebrew

```
brew install pyqt
```

#### 安装Qt

安装很简单，一路下一步，不用配置什么，默认的配置即可，只是用Qt的QtDesigner可执行程序，最后不用启动，直接关闭就行。

##### 方式一：本地安装

[http://download.qt.io/official_releases/qt/5.8/5.8.0/qt-opensource-mac-x64-clang-5.8.0.dmg](http://download.qt.io/official_releases/qt/5.8/5.8.0/qt-opensource-mac-x64-clang-5.8.0.dmg)

[http://download.qt.io/official_releases/qt/5.8/5.8.0/qt-opensource-linux-x64-5.8.0.run](http://download.qt.io/official_releases/qt/5.8/5.8.0/qt-opensource-linux-x64-5.8.0.run)

[http://download.qt.io/official_releases/qt/5.8/5.8.0/qt-opensource-windows-x86-msvc2015_64-5.8.0.exe](http://download.qt.io/official_releases/qt/5.8/5.8.0/qt-opensource-windows-x86-msvc2015_64-5.8.0.exe)



##### 方式二：使用Homebrew

```
brew install qt
```


到这里需要安装的都安装完成了，下面需要把所以安装的东西配置起来。

#### 配置Qt Designer

打开你的pycharm

![](http://p6dpqooos.bkt.clouddn.com/18-10-24/82978134.jpg)


#### 配置PyUIC
用于把QtDesigner创建的UI文件转换成py文件。

![](http://p6dpqooos.bkt.clouddn.com/18-10-24/91413758.jpg)

Parameters:参数

```
-m PyQt5.uic.pyuic  $FileName$ -o $FileNameWithoutExtension$.py
```


使用新创建的Python、PyQt5环境新建一个项目：

![](http://p6dpqooos.bkt.clouddn.com/18-10-24/13665698.jpg)

如下路径打开**Qt Designer程序**：

**`菜单栏 ->Tools->External Tools->Qt Designer`**

![](http://p6dpqooos.bkt.clouddn.com/18-10-24/21668429.jpg)

启动了**Qt Designer程序**，我们就可以拖控件了。

创建窗口程序，选择 **`Main Window`**，让后点击**`create`**。

![](http://p6dpqooos.bkt.clouddn.com/18-10-24/49825913.jpg)

点击**`create`**后，会出现画布和控件

![](http://p6dpqooos.bkt.clouddn.com/18-10-24/24273668.jpg)

**`保存`**布局文件。

![](http://p6dpqooos.bkt.clouddn.com/18-10-24/57155589.jpg)

在PyCharm中可以看到：

![](http://p6dpqooos.bkt.clouddn.com/18-10-24/50314264.jpg)

选择该 **`ui 文件`**， 如下操作：

![](http://p6dpqooos.bkt.clouddn.com/18-10-24/91932339.jpg)

这个**`命令行工具 PyUIC`** 就会把UI文件转成py文件。

![](http://p6dpqooos.bkt.clouddn.com/18-10-24/32100450.jpg)

启动这个python文件，我们需要调用它：

编写 **`main.py`**:

![](http://p6dpqooos.bkt.clouddn.com/18-10-24/72784404.jpg)

```
import sys
import HelloWorld
from PyQt5.QtWidgets import QApplication, QMainWindow

if __name__ == '__main__':
    app = QApplication(sys.argv)
    MainWindow = QMainWindow()
    ui = HelloWorld.Ui_MainWindow()
    ui.setupUi(MainWindow)
    MainWindow.show()
    sys.exit(app.exec_())
```
运行：

![](http://p6dpqooos.bkt.clouddn.com/18-10-24/86082366.jpg)

运行结果：

![](http://p6dpqooos.bkt.clouddn.com/18-10-24/47439591.jpg)


---
> 参考链接：
[https://www.jianshu.com/p/094928ac0b73](https://www.jianshu.com/p/094928ac0b73)