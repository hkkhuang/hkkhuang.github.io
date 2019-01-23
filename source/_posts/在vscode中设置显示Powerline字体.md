---
title: 在vscode中设置显示Powerline字体
date: 2019-01-23 21:53:40
tags: [VSCode, Tools]
categories: Tools
copyright: true
---

### 在iTerm中设置显示Powerline字体

在iTerm中设置了Powerline字体，在vscode中使用zsh终端会有字符显示不完整：

![](http://hexo-hkkhuang.oss-cn-shanghai.aliyuncs.com/18-11-30/3372288.jpg)

需要在VSCode中将字体改为Powerline字体.

<!--more-->

#### 下载安装字体
```
cd /Library/Fonts
git clone https://github.com/abertsch/Menlo-for-Powerline.git
```

#### VSCode配置Powerline字体
```
菜单栏 --> Code --> 首选项 --> 设置

菜单栏 --> Code --> Preferences --> Settings
```

选择左边栏**`Features --> Terminal`** ,之后选择右边对应的 **`Shell Args:Osx`** 进行设置， 点击**`Edit in settings.json`**进行设置：

![](http://hexo-hkkhuang.oss-cn-shanghai.aliyuncs.com/18-11-30/77816600.jpg)

或者通过搜索 **`Shell Args:Osx`**：

![](http://hexo-hkkhuang.oss-cn-shanghai.aliyuncs.com/18-11-30/33824394.jpg)

在 **`User Settings`** 中设置：

```
"terminal.integrated.fontFamily": "Menlo for Powerline",
```

![](http://hexo-hkkhuang.oss-cn-shanghai.aliyuncs.com/18-11-30/19670480.jpg)


