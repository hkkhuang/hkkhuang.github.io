---
title: 解决GitHub在push后显示灰色文件夹问题
date: 2018-06-06 13:56:11
tags: [Tools, github]
categories: github
copyright: true
---
**问题: push后文件夹显示灰色,无法访问.**

![](http://p6dpqooos.bkt.clouddn.com/18-4-24/70319110.jpg)
<!--more-->

1、因为子文件夹下还有git仓库，先删除文件夹中的**` .git .gitignore文件`**


2、在本地库中，将push后灰色文件夹剪切移除保存在其他路径下（不要删除）；

3、接下来依次执行以下命令：
```
git add .

git commit -m "xxx"

git push origin hexo
```
![](http://p6dpqooos.bkt.clouddn.com/18-4-24/61023918.jpg)

4、将第一步中保存到其他路径的的文件再次粘贴进来：

5、接下来再依次执行以下命令：
```
git add .

git commit -m "xxx"

git push origin hexo
```
![](http://p6dpqooos.bkt.clouddn.com/18-4-24/91279484.jpg)

![](http://p6dpqooos.bkt.clouddn.com/18-4-24/99986498.jpg)

6、大功告成！