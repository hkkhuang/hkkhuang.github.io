---
title: WARNING UNPROTECTED PRIVATE KEY FILE
date: 2019-11-27 14:20:45
tags: Tools
categories: Tools
copyright: true
---

# WARNING: UNPROTECTED PRIVATE KEY FILE!



## 问题描述

博客push时候出现**WARNING**，具体内容如下：

```bash
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0644 for '/Users/hkkhuang/.ssh/id_rsa' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "/Users/hkkhuang/.ssh/id_rsa": bad permissions
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
```

<!--more-->

可以看到提示：`“'/Users/hkkhuang/.ssh/id_rsa' are too open. It is required that your private key files are NOT accessible by others.”`



当前权限如下图：

![](http://cdn.hkkhuang.cn/20191127141655.png)

## 解决方法：

修改该文件权限：

```bash
cd ~/.ssh
chmod 400 id_rsa
```



修改后的权限如下图：
![](http://cdn.hkkhuang.cn/20191127141729.png)



再次push, 可以正常执行：

![](http://cdn.hkkhuang.cn/20191127141852.png)