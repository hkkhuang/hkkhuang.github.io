---
title: Mac配置LaTex(MacTex)以VSCode作为编辑器
date: 2019-01-22 14:43:00
tags: [VSCode, Latex, Tools]
categories: Tools
copyright: true
---
![](http://cdn.hkkhuang.cn/20190122144745.png)

### 相关软件的命令安装

可以使用 **`Homebrew`** 安装所需要的软件，Homebrew 的安装和使用参考其他文章。

#### 安装 Mactex 
选择MacTeX作为 LaTeX 编译引擎：

```
  brew cask install mactex
```

<!--more-->

#### 安装 VS Code 

选择VSCode作为LaTe 的编辑器

```
  brew cask install visual-studio-code
```

#### 安装 Skim 

选择Skim作为 PDF 浏览器

```
  brew cask install skim
```

### 安装MacTex
下载地址：[https://www.tug.org/mactex/mactex-download.html](https://www.tug.org/mactex/mactex-download.html)

下载文件为：MacTeX.pkg （具体版本根据下载实际情况确定），直接安装步骤安装，直至完成。

### 安装并配置VS Code

#### 安装VS Code

下载地址：[https://code.visualstudio.com/Download](https://code.visualstudio.com/Download)

![](http://hexo-hkkhuang.oss-cn-shanghai.aliyuncs.com/18-11-28/75600378.jpg)

##### 安装LaTeX Workshop插件

打开 VS Code，搜索插件： **`LaTeX Workshop`**，点击安装（下图已经安装），并重启VS Code.

![](http://hexo-hkkhuang.oss-cn-shanghai.aliyuncs.com/18-11-28/14191970.jpg)

##### 修改 User Setting 配置

**`Code --> Performance --> Setting --> User Setting`**

可以使用关键字**`tools`** 或者**`recipes`**搜索：

![](http://hexo-hkkhuang.oss-cn-shanghai.aliyuncs.com/18-11-28/43927773.jpg)

**`LaTeX Workshop`** 默认的编译工具是 **`latexmk`**，根据需要修改所需的工具和命令，这里将其修改为中文环境最常用的 **`xelatex`**，根据需求进行修改。

使用如下内容配置：

```
{
    "latex-workshop.latex.recipes": [{
    "name": "xelatex",
    "tools": [
        "xelatex"
    ]
  }, {
    "name": "latexmk",
    "tools": [
        "latexmk"
    ]
  },
  
  {
    "name": "pdflatex -> bibtex -> pdflatex*2",
    "tools": [
        "pdflatex",
        "bibtex",
        "pdflatex",
        "pdflatex"
    ]
  }
  ],
  
  "latex-workshop.latex.tools": [{
  "name": "latexmk",
  "command": "latexmk",
  "args": [
    "-synctex=1",
    "-interaction=nonstopmode",
    "-file-line-error",
    "-pdf",
    "%DOC%"
  ]
  }, {
  "name": "xelatex",
  "command": "xelatex",
  "args": [
    "-synctex=1",
    "-interaction=nonstopmode",
    "-file-line-error",
    "%DOC%"
  ]
  }, {
  "name": "pdflatex",
  "command": "pdflatex",
  "args": [
    "-synctex=1",
    "-interaction=nonstopmode",
    "-file-line-error",
    "%DOC%"
  ]
  }, {
  "name": "bibtex",
  "command": "bibtex",
  "args": [
    "%DOCFILE%"
  ]
  }],
  "latex-workshop.view.pdf.viewer": "tab",
  "latex-workshop.latex.clean.fileTypes": [
  "*.aux",
  "*.bbl",
  "*.blg",
  "*.idx",
  "*.ind",
  "*.lof",
  "*.lot",
  "*.out",
  "*.toc",
  "*.acn",
  "*.acr",
  "*.alg",
  "*.glg",
  "*.glo",
  "*.gls",
  "*.ist",
  "*.fls",
  "*.log",
  "*.fdb_latexmk"
  ],
}
```

![](http://hexo-hkkhuang.oss-cn-shanghai.aliyuncs.com/18-11-28/12443308.jpg)


用于配置编译链，同样地放入设置区。第一个**`recipes`**为默认的编译工具，如需要使用**`bibtex`**可在编译时单击**VS Code界面左下角的小勾**，单击**`“Build LaTeX project”`**，选择**`“xe->bib->xe->xe”`**，或者直接将**`“xe->bib->xe->xe”`**的recipes放到第一位，即可以默认工具编译，但会比较慢。

根据需要自行按照格式添加自己需要的编译链。
```
"latex-workshop.latex.recipes": [
    {
        "name": "xelatex",
        "tools": [
            "xelatex"
        ]
    },
    {
        "name": "xe->bib->xe->xe",
        "tools": [
            "xelatex",
            "bibtex",
            "xelatex",
            "xelatex"
        ]
    }
],
```

配置完成后重启VSCode.

### 使用VSCode 编辑LaTeX文档

#### 打开下载的LaTeX模板文件夹（或者新建文件夹）

![](http://hexo-hkkhuang.oss-cn-shanghai.aliyuncs.com/18-11-28/44764265.jpg)

#### 选择一个LaTeX文件（或者新建一个LaTeX文件）

选择一个LaTex文件，在最下方，选择**`编译`**文件；
使用快捷键 **`Ctrl + Alt + B  编译`** ，**`Ctrl + Alt + V`**对生成的 PDF文件预览，**`Ctrl + 鼠标左键点击 PDF`** 反向定位到 tex 文本。

![](http://hexo-hkkhuang.oss-cn-shanghai.aliyuncs.com/18-11-28/71069881.jpg)

#### 编译LaTeX文件

选择**`Build LaTeX project`**

![](http://hexo-hkkhuang.oss-cn-shanghai.aliyuncs.com/18-11-28/7665867.jpg)

接着选择**`xelatex`**

![](http://hexo-hkkhuang.oss-cn-shanghai.aliyuncs.com/18-11-28/46946909.jpg)

编译文件成功后，可以预览生成的PDF文件：

![](http://hexo-hkkhuang.oss-cn-shanghai.aliyuncs.com/18-11-28/89155070.jpg)