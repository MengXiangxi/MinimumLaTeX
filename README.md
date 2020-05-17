# MinimumLaTeX

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

本项目旨在提供一个尽可能简单的模式，使一个没有开发经验的同学能够快速达到能够使用 `LaTeX + Git` 进行工作和协作的程度。

## 目的和动机

在科研工作中，我们需要频繁地进行协作。Git 为这种协作模式提供了良好的平台。但是，很多人习惯的工具链同开源社区的生态水土不服，无法发挥这种协作工具的最大效能。

为了让习惯于 `MS Office + 网盘` 模式的同学尽快融入，我制作了这个项目，希望能够帮助大家尽快适应新的工作模式。

## 工具链

* Microsoft Windows 10 64 bit 相信这是最常用的系统。macOS 也差不太多，可自行摸索。操作系统也许是全部工具链中唯一非自由（或者是开源）软件的环节。
* [GitHub](https://github.com/) 实际上在工作中更多使用的是私有服务器上的 GitLab，但为了公开，暂使用GitHub替代。原理是一样的。
* [TeX Live](https://www.tug.org/texlive/) 倍受好评的 LaTeX 发行版。macOS 系统可使用 MacTeX 等系统替代。
* [Git for Windows](https://git-scm.com/download/win) Git 工具。
* [Visual Studio Code](https://code.visualstudio.com/) 也是微软旗下的编辑器，我个人青睐的。简称 VSCode 或 VSC。
* （可选）[GitHub Desktop](https://desktop.github.com/) Git 的 GUI，比 VScode 中的 Git 功能要更直观些。

## 计划

* 环境的配置
  * 软件下载与安装
  * VSCode 功能和插件介绍
* LaTeX 初步
  * LaTeX 基本概念与设定
  * LaTeX 的编辑进阶
  * 参考文献的插入
* GitHub 的使用
  * GitHub 基本操作
  * GitHub 的权限管理
  * GitHub Markdown
  
## 环境的配置

### 软件的下载和安装

* [TeX Live](https://www.tug.org/texlive/) 建议选择完整安装。
* [Visual Studio Code](https://code.visualstudio.com/)
* [Git for Windows](https://git-scm.com/download/win) 注意选择“Commit As-is”选项。
* [GitHub Desktop](https://desktop.github.com/)

### VSCode 功能和插件介绍

* VSCode 的基本界面及其功能，编辑区、侧边栏、Terminal。
* Preference、User Settings。
* 用 VSCode 写 Markdown，使用 `Markdown All in One` 插件。

```markdown
# Title

## Section

This is the text

| 123 | 456 |
| --- | --- |
| 000 | 111 |

```

* 尝试用 VSCode 编译 python，使用 `python` 插件。

```python
import os

print("Hello world!")
print(os.getcwd())
```

## LaTeX 初步

### LaTeX 基本概念与设定

* LaTeX 是干啥的？一种基于命令的排版工具。
* Knuth 创立 TeX，而 LaTeX 是在 TeX 基础上的一个宏集。
* TeX Live 集成了一堆编译器，把 `.tex` 文件中的代码编译成 PDF 文件。
* 在 VSCode 中使用 TeXLive，建议用 `LaTeX-Workshop` 插件。在 `Preference - User Setting` 中，打开 `settings.json`，修改其中的内容。以下内容供参考。

```json
    "latex-workshop.latex.tools": [
        {
            "name": "xelatex",
            "command": "xelatex",
            "args":[
                "%DOC%"
            ]
        },
        {
            "name": "dvipdf",
            "command": "dvipdfmx",
            "args":[
                "%DOC%"
            ],
        },
        {
            "command": "latexmk",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "%DOC%"
            ],
            "name": "latexmk"
        },
        {
            "name":"latex",
            "command":"latex",
            "args":[
                "%DOC%"
            ]
        },
        {
            "name":"dvips",
            "command":"dvips",
            "args":[
                "%DOCFILE%.dvi"
            ]
        },
        {
            "name":"ps2pdf",
            "command":"ps2pdf",
            "args":[
                "%DOCFILE%.ps"
            ]
        },
        {
            "name":"pdf2eps",
            "command":"pfd2esp",
            "args":[
                "1",
                "%DOC%"
            ]
        },
        {
            "name":"pdflatex",
            "command":"pdflatex",
            "args":[
                "-synctex=1",
                "%DOC%"
            ]
        },
        {
            "name":"bibtex",
            "command":"bibtex",
            "args":[
                "%DOCFILE%"
            ]
        }
    ],
    "latex-workshop.latex.recipes": [
        {
            "name": "pdflatex",
            "tools":[
                "pdflatex",
                "bibtex",
                "pdflatex",
                "pdflatex"
            ]
        },
        {
            "name": "PSTricks",
            "tools":[
                "latex",
                "dvips",
                "ps2pdf"
            ]
        },
        {
            "name": "PKUThesis",
            "tools": [
                "xelatex",
                "biber-pkuthss",
                "xelatex",
                "xelatex"
            ]
        },
        {
            "name": "xelatex-1",
            "tools": [
                "xelatex"
            ]
        },
        {
            "name": "pdflatex-1",
            "tools": [
                "pdflatex"
            ]
        },
        {
            "name": "index-pdflatex",
            "tools": [
                "makeindex",
                "pdflatex"
            ]
        },
        {
            "name": "index-xelatex",
            "tools": [
                "makeindex",
                "xelatex"
            ]
        }
    ],
```

* 此时建立一个 `.tex` 文件，可以看到侧边栏有一个 LaTeX 选项卡。我们可以尝试用这些命令来运行下面的 LaTeX 代码。

```tex
\documentclass[a4paper,12pt]{article}

\begin{document}
    \title{Title}
    \author{Meng, Xiangxi}
    \date{}
    \maketitle
    
    \section{The section}

    The contents.
    
    PDFLaTeX.
\end{document}
```

参考：[使用VSCode编写LaTeX](https://zhuanlan.zhihu.com/p/38178015)

### LaTeX 的编辑进阶

* LaTeX 代码的组成部分。
  
```tex
% 导言区 preamble
\documentclass[a4paper,12pt]{article} % 文档类

% 可用 `\usepackage{}` 语句插入宏包

\begin{document} % 正文部分
    \title{Title}
    \author{Meng, Xiangxi}
    \date{}
    \maketitle % 打印标题
    
    \section{The section} % 文档标题结构

    The contents.
    
    PDFLaTeX.
\end{document}
```

* LaTeX 的编译过程。

* 插入图片。浮动体的概念。

```tex
\usepackage{graphicx} % preamble

\begin{figure}[htbp]
    \centering
    \includegraphics[scale = 1]{test.png}
    \caption{Figure Caption}
    \label{fig:test}
\end{figure}
```

* 插入公式。
* 插入表格（留作自己探索）。

```tex
\usepackage{booktabs} % preamble

\begin{table}[htbp] 
 \caption{\label{tab:test}Test Table} 
 \begin{tabular}{lcl} 
  \toprule 
  Item 1 & Item 2 & Item 3  \\ 
  \midrule 
    1    &    2   &    3    \\ 
    4    &    5   &    6    \\ 
  \bottomrule 
 \end{tabular} 
\end{table}
```

### 参考文献的插入

## GitHub 的使用

### GitHub 基本操作

### GitHub 的权限管理
