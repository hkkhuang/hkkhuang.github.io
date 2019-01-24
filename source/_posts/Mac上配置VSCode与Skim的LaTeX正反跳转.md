---
title: Mac上配置VSCode与Skim的LaTeX正反跳转
date: 2019-01-24 17:52:39
tags: [VSCode, Latex, Tools]
categories: Tools
copyright: true
---

![](http://cdn.hkkhuang.cn/20190122144745.png)

### 正向搜索
正向搜索指的是从 .tex 源文件向编译生成的 PDF 文件的跳转。这部分我们主要需要寻找到合适的方式，在命令行状态打开 Skim 应用。

根据 Skim 官网的介绍，Skim 提供了名为 displayline 的脚本，用于和 TeX 正反同步协同工作。其脚本位于:

```
/Applications/Skim.app/Contents/SharedSupport/displayline
```

<!--more-->

具体用法是:

```
/Applications/Skim.app/Contents/SharedSupport/displayline %line "%pdffile" "%texfile"
```

此处 **`%line`** 表示 **`.tex`** 文件的行号，**`%pdffile`** 表示编译生成的 PDF 文件的完整路径，**`%texfile `**则是对应的 .tex 源文件。考虑到我们对反向搜索也有需求，按照官方文档，我们还需要加上**` -r `**参数。

因此，在 VSCode 的配置里，我们需要给出这样的 **`JSON 配置`**:

```
"latex-workshop.view.pdf.viewer": "external",
"latex-workshop.view.pdf.external.synctex": {
    "command": "/Applications/Skim.app/Contents/SharedSupport/displayline",
    "args": [
        "-r",
        "%LINE%",
        "%PDF%",
        "%TEX%"
    ]
},
```

**`LaTeX workshop `**插件的配置中，除了 **`latex-workshop.view.pdf.external.synctex`**，还有一项也和打开外部 PDF 浏览器有关。它是 **`latex-workshop.view.pdf.external.command`**，表示简单地打开 PDF 文件，而忽略正向搜索功能。**`Skim `**提供的命令行脚本默认不支持这样的操作，我们需要根据**` displayline `**脚本自行修改。

**`displayline `**脚本调用了 **`Apple Script`** 来实现与 **`Skim.app`** 的交互，此处我们照葫芦画瓢，模拟一个即可。我们可以将如下脚本保存为 **`displayfile`** 并以 **`chmod u+x displayfile`** 使其变为可执行脚本，而后将其放在**`环境变量 PATH`** 包含的目录中。

```
#!/bin/bash

# displayfile (Skim)
#
# Usage: displayfile [-r] [-g] PDFFILE
#
# Modified from "displayline" to only revert the file, not jump to a given line
#

if [ $# == 0 -o "$1" == "-h" -o "$1" == "-help" ]; then
  echo "Usage: displayfile [-r] [-g] PDFFILE
Options:
-r, -revert      Revert the file from disk if it was open
-g, -background  Do not bring Skim to the foreground"
  exit 0
fi

# get arguments
revert=false
activate=true
while [ "${1:0:1}" == "-" ]; do
  if [ "$1" == "-r" -o "$1" == "-revert" ]; then
    revert=true
  elif [ "$1" == "-g" -o "$1" == "-background" ]; then
    activate=false
  fi
  shift
done
file="$1"
#shopt -s extglob
#[ $# -gt 2 ] && source="$3" || source="${file%.@(pdf|dvi|xdv)}.tex"

# expand relative paths
[ "${file:0:1}" == "/" ] || file="${PWD}/${file}"

# pass file arguments as NULL-separated string to osascript
# pass through cat to get them as raw bytes to preserve non-ASCII characters
/usr/bin/osascript \
  -e "set theFile to POSIX file \"$file\"" \
  -e "set thePath to POSIX path of (theFile as alias)" \
  -e "tell application \"Skim\"" \
  -e "  if $activate then activate" \
  -e "  if $revert then" \
  -e "    try" \
  -e "      set theDocs to get documents whose path is thePath" \
  -e "      if (count of theDocs) > 0 then revert theDocs" \
  -e "    end try" \
  -e "  end if" \
  -e "  open theFile" \
  -e "end tell"
```

至此，需要更新 VSCode 的配置。

```
"latex-workshop.view.pdf.external.command": {
    "command": "displayfile",
    "args": [
        "-r",
        "%PDF%"
    ]
},
```

### 反向搜索

在反向搜索中，我们需要让 Skim 能够打开 VSCode，并将文件名和相应的行号正确地传给 VSCode。根据 Skim 官网的介绍，它只会从**` /usr/bin `**和 **`/usr/local/bin`** 中检索可执行程序。为此，我们需要将 VSCode 的可执行程序软链到这两个目录中的一个当中。

```
ln -sf /Applications/Visual\ Studio\ Code.app/Contents/MacOS/Electron /usr/local/bin/vscode
```

至此，我们在命令行中执行 **`vscode -g "%file":%line`** 即可打开 **`%file`** 文件并定位到第 **`%line`** 行。于是，我们只需要在 Skim 的同步配置中将预设改为「自定义」，并将命令和参数分别设置如下：

```
Command: vscode
Arguments: -g "%file":%line
```

如此即完成了配置。