---
title: Proverif Installation
date: 2019-01-21 21:35:18
tags: [ProVerif, Tools]
categories: Tools
copyright: true
---

ProVerif is compatible with the Linux, Mac, and Windows operating systems; it can be downloadedfrom:

[http://proverif.inria.fr/](http://proverif.inria.fr/)

The remainder of this section covers installation on Linux,Mac, and Windows platforms.

### Installation via OPAM

ProVerif has been developed using Objective Caml (OCaml) and OPAM is the package manager ofOCaml. Installing via OPAM is the simplest, especially if you already have OPAM installed.

#### OPAM installed

If you do not already have OPAM installed, download it from

[https://opam.ocaml.org/](https://opam.ocaml.org/)

and install it.

or 

```
brew install opam
```


#### opam update

If you already have OPAM installed, run

```
opam update
```

Opam has not been initialised, please run `opam init'

```
opam init  
```

to make sure that you get the latest version of ProVerif.

![](http://cdn.hkkhuang.cn/20190121150709.png)

![](http://cdn.hkkhuang.cn/20190121150939.png)

![](http://cdn.hkkhuang.cn/20190121151016.png)

#### Run

```
opam depext conf-graphviz
opam depext proverif
opam install proverif
```

⚠️⚠️**注意：**

The first line installs graphviz, if you do not already have it. You may also install it using thepackage manager of your Linux, OSX, or cygwin distribution,especially if opam fails to install it.It is needed only for the graphical display of attacks. 

The second line installs **`GTK+2`** including development libraries, if you do not already have it. You mayalso install it using the packagemanager of your distribution. It is needed for the interactive simulatorproverifinteract. 【 [见问题处理] (#problem) 】

Thethird line installs ProVerif itself and its OCaml dependencies.  ProVerif executables are in~/.opam/〈switch〉/bin, which is in thePATH, examples are in~/.opam/〈switch〉/doc/proverif, andvarious helper files are in~/.opam/〈switch〉/share/proverif. The directory〈switch〉is the opamswitch in which you installed ProVerif, by defaultsystem.


01![](http://cdn.hkkhuang.cn/20190121151326.png)

02![](http://cdn.hkkhuang.cn/20190121151644.png)

03![](http://cdn.hkkhuang.cn/20190121154350.png)


![](http://cdn.hkkhuang.cn/20190121153259.png)

#### <span id="problem">⚠️问题处理</span>

![](http://cdn.hkkhuang.cn/20190121154601.png)

##### Mac上配置GTK

GTK version 2+

```
brew install pkg-config
brew install gtk+3   or   brew install gtk+
```