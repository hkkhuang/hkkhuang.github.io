---
title: iTerm2及oh-my-zsh的安装及配置
date: 2018-11-06 10:55:43
tags: [Terminal，Tools]
categories: Tools
copyright: true
---

![](http://p6dpqooos.bkt.clouddn.com/18-11-6/86476104.jpg)

### 1. 安装 iTerm2

（1） 直接下载安装文件

下载地址：[https://www.iterm2.com/downloads.html](https://www.iterm2.com/downloads.html)

解压下载的压缩文件，将其拖到 `Applications` 目录下，直接双击打开。

（2）使用 Homebrew 进行安装：

```
brew cask install iterm2
```

（3）**mac系统**内置了zsh，查看内置shell：

```
cat /etc/shells
```

<!--more-->

![](http://p6dpqooos.bkt.clouddn.com/18-11-6/89748342.jpg)

### 2. 配置 iTerm2 主题

iTerm2 最常用的主题是 **Solarized Dark theme**.

下载地址：[http://ethanschoonover.com/solarized](http://ethanschoonover.com/solarized)

1. 解压下载的压缩文件；

1. 打开 **iTerm2**，使用快键键 `Command + ,` 键，或者 `iTerm2 -> Preferences` 打开**Preferences**配置界面；

1. 按照 `Profiles -> Colors -> Color Presets -> Import`操作，导入刚刚下载解压的主题文件：`solarized->iterm2-colors-solarized->Solarized Dark.itermcolors`文件；

1. 导入成功，选择 Solarized Dark 主题。

![](http://p6dpqooos.bkt.clouddn.com/18-11-6/45350933.jpg)

### 3. 配置 Oh My Zsh

Oh My Zsh地址： [https://github.com/robbyrussell/oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)

Oh My Zsh 是对主题的进一步扩展；

下载地址：[https://github.com/robbyrussell/oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)

* 一键安装：

```
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

* 安装完成后需要把 zsh 设置为默认 Shell：

```
sudo chsh -s /bin/zsh
```

重新启动iTerm2，zsh就已经被配置成默认的shell了.

> **注意：上面的命令必须用管理员权限运行，不然无法配置**

> 提示：chsh: no changes made

* 将主题配置修改为 **`ZSH_THEME="agnoster`**（根据自己喜好设置主题）:

	* zsh 主题列表：[https://github.com/robbyrussell/oh-my-zsh/tree/master/themes](https://github.com/robbyrussell/oh-my-zsh/tree/master/themes)
	

```
vim ~/.zshrc
```

![](http://p6dpqooos.bkt.clouddn.com/18-11-6/50079031.jpg)

* 更改主题之后，重启iterms2后，效果如下：

![](http://p6dpqooos.bkt.clouddn.com/18-11-6/44665832.jpg)

**`问号 ❓`**  什么鬼？？？

第一直觉肯定是字符编码问题，事实也是如此，哈哈哈。

### 4. 解决显示 “`问号 ❓`” 问题

没有没有图片中的箭头，那是因为产生箭头效果是需要特殊字体支持的，这个字体最开始是一个叫**`Powerline`**的项目开始的，其目的是美化Vim中操作栏的字体状态使其产生箭头效果，也被移植到了iTerm2上。

* **Powerline字体下载安装**

github项目地址：[https://github.com/yizhen20133868/fonts](https://github.com/yizhen20133868/fonts)

安装Powerline字体，使用如下命令：

```
# clone
git clone https://github.com/powerline/fonts.git


cd fonts

# install
./install.sh
```

![](http://p6dpqooos.bkt.clouddn.com/18-11-6/46222177.jpg)

安装完字体库之后，设置iTerm 2的字体：

**`Profile->Text`** 选项卡中里的 **`Regular Font`**和**`Non-ASCII Font`**的字体都设置成 Powerline的字体，这里设置的字体是**`Meslo LG S DZ Regular for Powerline`**:

![](http://p6dpqooos.bkt.clouddn.com/18-11-6/28867379.jpg)

配置完成效果：

![](http://p6dpqooos.bkt.clouddn.com/18-11-6/38871667.jpg)

**参考：**

[https://www.cnblogs.com/xishuai/p/mac-iterm2.html](https://www.cnblogs.com/xishuai/p/mac-iterm2.html)

[https://zhuanlan.zhihu.com/p/26373052](https://zhuanlan.zhihu.com/p/26373052)




