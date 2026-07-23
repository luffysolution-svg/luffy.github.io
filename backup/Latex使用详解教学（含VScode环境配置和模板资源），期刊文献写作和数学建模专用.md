<html>
<body>
<!--StartFragment--><!-- obsidian --><h1 data-heading="一、需要配置的内容">一、需要配置的内容</h1>
<p>需要安装三部分：</p>

组件 | 作用
-- | --
TeX Live | 提供 XeLaTeX、PDFLaTeX、LuaLaTeX、latexmk、BibTeX、Biber 和宏包
VS Code | 编辑器
LaTeX Workshop | 在 VS Code 中调用 TeX Live、预览 PDF、代码补全和 SyncTeX

<!--EndFragment-->
</body>
</html># 一、需要配置的内容

需要安装三部分：

| 组件             | 作用                                                    |
| -------------- | ----------------------------------------------------- |
| TeX Live       | 提供 XeLaTeX、PDFLaTeX、LuaLaTeX、latexmk、BibTeX、Biber 和宏包 |
| VS Code        | 编辑器                                                   |
| LaTeX Workshop | 在 VS Code 中调用 TeX Live、预览 PDF、代码补全和 SyncTeX           |

注意：**LaTeX Workshop 本身不是编译器**。仅安装扩展而没有安装 TeX Live，无法编译。

---

# 二、安装 VS Code

## 1. 下载官方版本

https://code.visualstudio.com/

![PixPin_2026-07-23_14-24-38.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-07-23_14-24-38.png)

## 2. 安装选项

运行安装程序时，建议勾选：

```text
添加到 PATH
将“通过 Code 打开”添加到 Windows 资源管理器文件上下文菜单
将“通过 Code 打开”添加到目录上下文菜单
将 Code 注册为受支持文件类型的编辑器
```

安装完成后，关闭并重新打开 PowerShell，测试：

```powershell
code --version
```

注意：CMD和Powershell可以通过`Win`+`R`弹出窗口后输入cmd或者powershell使用

![PixPin_2026-07-23_14-23-45.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-07-23_14-23-45.png)

![PixPin_2026-07-23_14-26-18.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-07-23_14-26-18.png)

能够显示版本号即正常。

---

# 三、安装最新稳定版本 TeX Live 

## 1. 为什么选择 TeX Live

对于数学建模和期刊论文，建议使用 TeX Live 完整版，原因是：

- 包含绝大多数常见宏包
- Windows 版自带 Perl，可直接运行 `latexmk`
- 包含 XeLaTeX、PDFLaTeX、LuaLaTeX
- 包含 BibTeX、Biber
- 不依赖编译时临时下载宏包

LaTeX Workshop 官方推荐 TeX Live；MiKTeX 虽然体积较小，但 `latexmk` 还需要额外处理 Perl 环境。

![PixPin_2026-07-23_14-48-21.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-07-23_14-48-21.png)

官方下载地址
https://www.latex-project.org/get/

---

## 2. 选择国内镜像

### 推荐：清华大学 TUNA

https://mirrors.tuna.tsinghua.edu.cn/help/CTAN/

镜像目录：

```text
https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/tlnet/
```

Windows 安装器：

```text
https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/tlnet/install-tl-windows.exe
```

ZIP 安装器：

```text
https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/tlnet/install-tl.zip
```

清华镜像官方提供了 TeX Live 安装和 `tlmgr` 镜像配置方法。([[清华镜像站](https://mirrors.tuna.tsinghua.edu.cn/help/CTAN/)](https://mirrors.tuna.tsinghua.edu.cn/help/CTAN/ "Ctan | 镜像站使用帮助 | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror"))

### 备用：阿里云

```text
https://mirrors.aliyun.com/CTAN/systems/texlive/tlnet/
```

该目录提供当前 TeX Live 网络安装器和安装仓库。([[阿里云镜像](https://mirrors.aliyun.com/CTAN/systems/texlive/)](https://mirrors.aliyun.com/CTAN/systems/texlive/ "CTAN-systems-texlive安装包下载-开源镜像站-阿里云"))

### 自动选择 CTAN 镜像

```text
https://mirror.ctan.org/systems/texlive/tlnet/install-tl-windows.exe
```

`mirror.ctan.org` 会自动跳转到附近的 CTAN 镜像，但自动选择的节点不一定对当前网络最快。([[TeX Users Group](https://tug.org/texlive/acquire-netinstall.html)](https://tug.org/texlive/acquire-netinstall.html "Installing TeX Live over the Internet - TeX Users Group"))

---

## 3. 图形界面安装方法

下载：

```text
install-tl-windows.exe
```

双击运行，然后：

1. 选择 **Install**。
2. 进入 TeX Live 安装界面。
3. 点击 **Advanced**。
4. 检查或修改 Repository。
5. 选择安装方案。
6. 设置安装路径。
7. 开始安装。

### 推荐设置

| 项目                    | 推荐值               |
| --------------------- | ----------------- |
| Repository            | 清华 TUNA           |
| Selected scheme       | `scheme-full`     |
| Installation root     | `C:\texlive\2026` |
| Default paper size    | A4                |
| Install documentation | 保留                |
| Install source files  | 可取消，节省空间          |
| Create shortcuts      | 可选                |
| Adjust PATH           | 开启或保持默认           |

### 安装路径要求

建议使用：

```text
C:\texlive\2026
```

TeX Live 官方明确建议 Windows 安装路径避免中文等非 ASCII 字符。([[TeX Users Group](https://www.tug.org/texlive/doc/texlive-en/texlive-en.html)](https://www.tug.org/texlive/doc/texlive-en/texlive-en.html "The TeX Live Guide—2026"))

---

## 4. 使用命令行强制指定镜像

若图形安装器下载较慢，可以下载：

```text
install-tl.zip
```

解压到纯英文目录，例如：

```text
C:\Temp\install-tl
```

在该文件夹打开 PowerShell，运行：

```powershell
.\install-tl-windows.bat -repository https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/tlnet
```

安装器支持通过 `-repository` 明确指定仓库。([[TeX Users Group](https://tug.org/texlive/doc/texlive-en/texlive-en.html?utm_source=chatgpt.com)](https://tug.org/texlive/doc/texlive-en/texlive-en.html?utm_source=chatgpt.com "The TeX Live Guide—2026"))

---

# 四、检查 TeX Live 是否安装成功

安装完成后：

1. 完全关闭 VS Code。
2. 关闭所有 PowerShell 和 CMD。
3. 重新打开 PowerShell。

依次执行：

```powershell
xelatex --version
pdflatex --version
lualatex --version
latexmk -v
bibtex --version
biber --version
chktex -v
latexindent -v
```

![PixPin_2026-07-23_14-24-09.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-07-23_14-24-09.png)


检查实际路径：

```powershell
where.exe xelatex
where.exe latexmk
where.exe biber
```

正常情况下应指向类似：

```text
C:\texlive\2026\bin\windows\xelatex.exe
C:\texlive\2026\bin\windows\latexmk.exe
C:\texlive\2026\bin\windows\biber.exe
```

## 如果提示“无法识别命令”

将以下目录添加到 Windows `Path`：

```text
C:\texlive\2026\bin\windows
```

操作路径：

```text
设置
→ 系统
→ 系统信息
→ 高级系统设置
→ 环境变量
→ 用户变量或系统变量中的 Path
→ 新建
```

添加后重新启动 VS Code。LaTeX Workshop 只调用系统 `PATH` 中的程序，不会自行修复 TeX Live 环境变量。([[GitHub](https://github.com/James-Yu/latex-workshop/wiki/Install?utm_source=chatgpt.com)](https://github.com/James-Yu/latex-workshop/wiki/Install?utm_source=chatgpt.com "Install · James-Yu/LaTeX-Workshop Wiki · GitHub"))

---

# 五、安装 LaTeX Workshop

（Windows）打开 VS Code，按：

```text
Ctrl + Shift + X
```

搜索：

```text
LaTeX Workshop
```
![PixPin_2026-07-23_14-20-59.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-07-23_14-20-59.png)

确认：

```text
名称：LaTeX Workshop
发布者：James Yu
扩展 ID：James-Yu.latex-workshop
```

然后点击安装。

也可以在 PowerShell 中执行：

```powershell
code --install-extension James-Yu.latex-workshop
```

VS Code 支持通过扩展 ID 安装扩展；当前 LaTeX Workshop 要求较新的 VS Code 版本，因此应使用当前官方 VS Code。([[Visual Studio Code](https://code.visualstudio.com/docs/configure/extensions/extension-marketplace)](https://code.visualstudio.com/docs/configure/extensions/extension-marketplace "Extension Marketplace"))

---

# 六、配置 `settings.json`

## 1. 打开配置文件

按：

```text
Ctrl + Shift + P
```

搜索：

```text
Preferences: Open User Settings (JSON)
```

![PixPin_2026-07-23_14-20-14.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-07-23_14-20-14.png)

如果原文件已经存在其他配置，不要重复写最外层 `{}`，只把对应属性合并进去。

## 2. 推荐完整配置

```jsonc
{
    // ==============================
    // LaTeX 自动编译
    // ==============================

    // 保存 .tex 文件时自动编译
    "latex-workshop.latex.autoBuild.run": "onSave",

    // 使用上一次手动选择的编译方案
    "latex-workshop.latex.recipe.default": "lastUsed",

    // PDF 和辅助文件统一放入 build 文件夹
    "latex-workshop.latex.outDir": "%DIR%/build",

    // 显示当前识别到的主文件
    "latex-workshop.latex.build.rootfileInStatus": true,

    // 允许识别 % !TEX root 等魔法注释
    "latex-workshop.latex.build.enableMagicComments": true,

    // 编译失败后清理辅助文件并重试一次
    "latex-workshop.latex.autoBuild.cleanAndRetry.enabled": true,

    // 不在成功编译后自动删除日志和辅助文件
    "latex-workshop.latex.autoClean.run": "never",

    // ==============================
    // 编译方案
    // ==============================

    "latex-workshop.latex.recipes": [
        {
            "name": "latexmk (XeLaTeX)",
            "tools": [
                "latexmk-xelatex"
            ]
        },
        {
            "name": "latexmk (PDFLaTeX)",
            "tools": [
                "latexmk-pdflatex"
            ]
        },
        {
            "name": "latexmk (LuaLaTeX)",
            "tools": [
                "latexmk-lualatex"
            ]
        }
    ],

    // ==============================
    // 编译工具
    // ==============================

    "latex-workshop.latex.tools": [
        {
            "name": "latexmk-xelatex",
            "command": "latexmk",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-xelatex",
                "-outdir=%OUTDIR%",
                "%DOC%"
            ],
            "env": {}
        },
        {
            "name": "latexmk-pdflatex",
            "command": "latexmk",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-pdf",
                "-outdir=%OUTDIR%",
                "%DOC%"
            ],
            "env": {}
        },
        {
            "name": "latexmk-lualatex",
            "command": "latexmk",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-lualatex",
                "-outdir=%OUTDIR%",
                "%DOC%"
            ],
            "env": {}
        }
    ],

    // ==============================
    // PDF 预览和 SyncTeX
    // ==============================

    // 使用 VS Code 内置 PDF 阅读器
    "latex-workshop.view.pdf.viewer": "tab",

    // PDF 默认在右侧显示
    "latex-workshop.view.pdf.tab.editorGroup": "right",

    // 默认适应页面宽度
    "latex-workshop.view.pdf.zoom": "page-width",

    // 编译后不强制跳动 PDF 页面
    "latex-workshop.synctex.afterBuild.enabled": false,

    // ==============================
    // 检查与格式化
    // ==============================

    // 检查重复 label
    "latex-workshop.check.duplicatedLabels.enabled": true,

    // 默认关闭 ChkTeX，避免初学阶段出现大量排版建议
    "latex-workshop.linting.chktex.enabled": false,

    // 启用 latexindent 作为手动格式化工具
    "latex-workshop.formatting.latex": "latexindent",

    // ==============================
    // 编辑器设置
    // ==============================

    "[latex]": {
        "editor.wordWrap": "on",
        "editor.tabSize": 2,
        "editor.insertSpaces": true,
        "editor.formatOnSave": false
    },

    "[bibtex]": {
        "editor.tabSize": 2,
        "editor.insertSpaces": true,
        "editor.wordWrap": "on"
    }
}
```

LaTeX Workshop 的 recipe 是一组按顺序调用的编译工具；`latexmk` 是默认且推荐的构建方式，可以管理重复编译和参考文献依赖。`first` 和 `lastUsed` 都是官方支持的默认 recipe 选择方式

内置 PDF 阅读器支持源码到 PDF、PDF 到源码的 SyncTeX 定位。

---

# 八、创建测试文件

## 1. `test.tex`

```latex
\documentclass[UTF8,a4paper,12pt]{ctexart}

\usepackage{amsmath}
\usepackage{amssymb}
\usepackage{booktabs}
\usepackage{graphicx}
\usepackage{siunitx}

\usepackage[
  backend=biber,
  style=numeric,
  sorting=none
]{biblatex}

\addbibresource{refs.bib}

\usepackage[
  colorlinks=true,
  linkcolor=blue,
  citecolor=blue,
  urlcolor=blue
]{hyperref}

\title{VS Code 与 LaTeX 环境测试}
\author{Luffy}
\date{\today}

\begin{document}

\maketitle

\tableofcontents

\section{中文测试}

这是一段中文内容，用于测试 \LaTeX{} 中文排版。

\section{数学公式}

爱因斯坦质能方程为

\begin{equation}
  E = mc^2.
\end{equation}

一个简单的优化模型为

\begin{align}
  \min_{x_1,x_2}\quad
  & f(x_1,x_2)=x_1^2+x_2^2, \\
  \text{s.t.}\quad
  & x_1+x_2\geq 1, \\
  & x_1,x_2\geq 0.
\end{align}

\section{表格测试}

\begin{table}[htbp]
  \centering
  \caption{实验数据示例}
  \label{tab:data}
  \begin{tabular}{lcc}
    \toprule
    样品 & 温度 & 转化率 \\
    \midrule
    A & 300 & 82.5\% \\
    B & 350 & 91.2\% \\
    \bottomrule
  \end{tabular}
\end{table}

表~\ref{tab:data} 展示了测试数据。

\section{参考文献测试}

LaTeX 是常用的科技文档排版系统\cite{lamport1994}。

\printbibliography

\end{document}
```

## 2. `refs.bib`

```bibtex
@book{lamport1994,
  author    = {Leslie Lamport},
  title     = {LaTeX: A Document Preparation System},
  edition   = {2},
  publisher = {Addison-Wesley},
  year      = {1994}
}
```

---

# 九、编译

## 1. 确保当前窗口是 `test.tex`

点击：

```text
test.tex
```

根据中英文情况选择编译方案

## 2. 执行编译

快捷键：

```text
Ctrl + Alt + B
```

成功后会生成：

```text
build/test.pdf
```

## 3. 打开 PDF

快捷键：

```text
Ctrl + Alt + V
```

## 4. 正向定位

将光标放在 `.tex` 源码某一行，按：

```text
Ctrl + Alt + J
```

PDF 会跳转到对应位置。

## 5. 反向定位

在 VS Code 内置 PDF 中：

```text
Ctrl + 鼠标左键
```


---

# 十、不同场景如何选择编译器

| 使用场景                | 编译方案                |
| ------------------- | ------------------- |
| 中文数学建模              | `latexmk (XeLaTeX)` |
| 中文学位论文              | 优先按模板说明，通常 XeLaTeX  |
| 英文数学建模              | 通常 PDFLaTeX         |
| 国外期刊模板              | 按期刊模板说明             |
| 使用 `fontspec`       | XeLaTeX 或 LuaLaTeX  |
| 使用系统中文字体            | XeLaTeX 或 LuaLaTeX  |
| 传统 `.cls`、`.bst` 模板 | 通常 PDFLaTeX         |
| `biblatex + biber`  | 三种引擎均可，交给 latexmk   |
| `natbib + bibtex`   | 三种引擎均可，交给 latexmk   |

不要为了统一而强行用 XeLaTeX 编译所有模板。期刊模板明确要求 PDFLaTeX 时，应切换到：

```text
latexmk (PDFLaTeX)
```

---

# 十一、多文件论文配置

项目结构：

```text
paper/
├─ main.tex
├─ refs.bib
├─ chapters/
│  ├─ introduction.tex
│  ├─ methods.tex
│  └─ results.tex
├─ figures/
└─ build/
```

`main.tex`：

```latex
\documentclass{ctexart}

\begin{document}

\input{chapters/introduction}
\input{chapters/methods}
\input{chapters/results}

\end{document}
```

在 `chapters/introduction.tex` 第一行写：

```latex
% !TEX root = ../main.tex
```

这样即使当前编辑的是子文件，LaTeX Workshop 也会编译 `main.tex`。根文件魔法注释是官方支持的识别机制。

---

# 十二、可选：开启语法检查

确认以下命令正常：

```powershell
chktex -v
```

然后在 `settings.json` 中修改：

```jsonc
"latex-workshop.linting.chktex.enabled": true,
"latex-workshop.linting.run": "onSave"
```

ChkTeX 会检查常见 LaTeX 书写和排版问题，并把结果显示在 VS Code 的“问题”面板，但部分警告只是风格建议，并不代表无法编译。

---

# 十三、可选：格式化 LaTeX

确认：

```powershell
latexindent -v
```

然后打开 `.tex` 文件，按：

```text
Shift + Alt + F
```

LaTeX Workshop 可以调用 `latexindent` 格式化 LaTeX 源码。([[GitHub](https://github.com/James-Yu/latex-workshop/wiki/Format?utm_source=chatgpt.com)](https://github.com/James-Yu/latex-workshop/wiki/Format?utm_source=chatgpt.com "Format · James-Yu/LaTeX-Workshop Wiki · GitHub"))

不建议刚开始就启用：

```jsonc
"editor.formatOnSave": true
```

复杂期刊模板中，自动格式化可能造成大量无意义的代码差异。

---

# 十四、常见错误排查

## 1. `Cannot find LaTeX root file`

原因通常是当前活动窗口不是 `.tex` 文件。

处理：

1. 点击 `test.tex`。
2. 确认包含：

```latex
\documentclass{...}
\begin{document}
```

3. 打开整个项目文件夹。
4. 子文件添加：
    

```latex
% !TEX root = ../main.tex
```

LaTeX Workshop 的根文件识别首先检查当前活动编辑器，因此在日志窗口触发编译会导致无法找到主文件。([[GitHub](https://github.com/james-yu/latex-workshop/wiki/compile?utm_source=chatgpt.com)](https://github.com/james-yu/latex-workshop/wiki/compile?utm_source=chatgpt.com "Compile · James-Yu/LaTeX-Workshop Wiki · GitHub"))

---

## 2. `spawn latexmk ENOENT`

原因：VS Code 找不到 `latexmk`。

检查：

```powershell
where.exe latexmk
latexmk -v
```

若找不到，将：

```text
C:\texlive\2026\bin\windows
```

加入 `Path`，然后彻底重启 VS Code。

---

## 3. `xelatex is not recognized`

检查：

```powershell
where.exe xelatex
```

仍然是 TeX Live 环境变量问题，不是 `.tex` 文件名问题。

---

## 4. `File xxx.sty not found`

安装缺失宏包：

```powershell
tlmgr search --global --file xxx.sty
```

根据搜索结果安装：

```powershell
tlmgr install 宏包名称
```

若使用 `scheme-full`，这种情况通常只会出现在非常新的或模板私有宏包中。

---

## 5. Biber 报错

检查：

```powershell
biber --version
```

清理项目：

```text
Ctrl + Alt + C
```

然后重新编译：

```text
Ctrl + Alt + B
```

同时检查：

```latex
\usepackage[backend=biber]{biblatex}
```

和：

```latex
\addbibresource{refs.bib}
```

文件名是否正确。

---

## 6. PDF 没有更新

依次执行：

```text
Ctrl + Alt + C
Ctrl + Alt + B
Ctrl + Alt + V
```

然后查看：

```text
查看 → 输出 → LaTeX Workshop
```

以及：

```text
build/test.log
```

---

## 7. 中文字体报错

初期不要自行指定：

```latex
\setCJKmainfont{某个字体}
```

先使用：

```latex
\documentclass[UTF8]{ctexart}
```

让 `ctex` 自动选择可用字体。确认基础环境正常后，再配置具体字体。

---

# 十五、期刊投稿注意事项

期刊提供模板时，通常会包含：

```text
journal-template/
├─ manuscript.tex
├─ journal.cls
├─ journal.bst
├─ references.bib
└─ figures/
```

处理原则：

1. 不要修改 `.cls` 和 `.bst`，除非期刊明确要求。
2. 不要把 `ctex` 强行加入英文期刊模板。
3. 按模板说明选择 PDFLaTeX、XeLaTeX 或 LuaLaTeX。
4. 使用期刊已有的参考文献命令。
5. 提交前检查期刊是否要求上传 `.bbl`。
6. 不要把本机绝对路径写入论文：

```latex
% 错误
\includegraphics{D:/MyFiles/paper/figures/a.png}

% 正确
\includegraphics{figures/a.png}
```

---

# 十六、期刊模板来源

## 1.GitHub搜索学校学位论文模板

https://github.com/search?q=Chinese+University+Thesis+LaTeX&type=repositories&p=2

![PixPin_2026-07-23_13-59-44.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-07-23_13-59-44.png)

## 2.学位论文Latex官方模板：

https://ctan.org/topic/dissertation

![PixPin_2026-07-23_14-00-21.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-07-23_14-00-21.png)


## 3.Latex官方文档模板

https://ctan.org/topic/doc-templ

![PixPin_2026-07-23_14-04-46.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-07-23_14-04-46.png)


## 4.Overleaf 模板

https://www.overleaf.com/latex/templates

![PixPin_2026-07-23_14-01-42.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-07-23_14-01-42.png)

## 5.Latex Template

https://www.latextemplates.com/

![PixPin_2026-07-23_14-07-00.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-07-23_14-07-00.png)

## 6.Latex工作室

https://www.latexstudio.net/

![PixPin_2026-07-23_14-07-55.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-07-23_14-07-55.png)


Overleaf 覆盖期刊文章、论文、简历、报告、演示和海报等类型；CTAN 则更适合获取宏包的正式版本、文档和源文件。

## 7.期刊出版社模板

| 出版社              | 官方入口                                                                                                                                 |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| IEEE             | [[IEEE Author Templates](https://journals.ieeeauthorcenter.ieee.org/create-your-ieee-journal-article/authoring-tools-and-templates/)](https://journals.ieeeauthorcenter.ieee.org/create-your-ieee-journal-article/authoring-tools-and-templates/)  |
| Elsevier         | [[Elsevier LaTeX Instructions](https://www.elsevier.com/en-gb/researcher/author/policies-and-guidelines/latex-instructions)](https://www.elsevier.com/en-gb/researcher/author/policies-and-guidelines/latex-instructions)           |
| Springer Nature  | [[Springer Nature LaTeX Support](https://www.springernature.com/gp/authors/campaigns/latex-author-support)](https://www.springernature.com/gp/authors/campaigns/latex-author-support)                            |
| Wiley            | [[Wiley LaTeX Template](https://authors.wiley.com/author-resources/Journal-Authors/Prepare/new-journal-design.html)](https://authors.wiley.com/author-resources/Journal-Authors/Prepare/new-journal-design.html)                   |
| Taylor & Francis | [[LaTeX Templates](https://authorservices.taylorandfrancis.com/publishing-your-research/writing-your-paper/formatting-and-templates/)](https://authorservices.taylorandfrancis.com/publishing-your-research/writing-your-paper/formatting-and-templates/) |

IEEE 提供按具体出版物选择模板的工具；Elsevier 使用 `elsarticle` 等官方文档类；Springer Nature 和 Wiley 也提供模板包，但都要求同时核对目标期刊自己的作者指南。

### 化学与材料方向

- [[ACS LaTeX 投稿模板与说明](https://pubs.acs.org/page/4authors/submission/tex.html)](https://pubs.acs.org/page/4authors/submission/tex.html)
- [[RSC 文章模板](https://www.rsc.org/publishing/publish-with-us/publish-a-journal-article/article-templates)](https://www.rsc.org/publishing/publish-with-us/publish-a-journal-article/article-templates)
- [[Elsevier LaTeX 模板](https://www.elsevier.com/en-gb/researcher/author/policies-and-guidelines/latex-instructions)](https://www.elsevier.com/en-gb/researcher/author/policies-and-guidelines/latex-instructions)
- [[Wiley 期刊 LaTeX 模板](https://authors.wiley.com/author-resources/Journal-Authors/Prepare/new-journal-design.html)](https://authors.wiley.com/author-resources/Journal-Authors/Prepare/new-journal-design.html)
- [[Springer Nature 模板](https://www.springernature.com/gp/authors/campaigns/latex-author-support)](https://www.springernature.com/gp/authors/campaigns/latex-author-support)

ACS 提供官方样式包和投稿文件要求；RSC 提供 Article、Communication 和 Faraday Discussions 等不同类型的 LaTeX 模板。


## 8. 数学建模模板

### MCM/ICM 美赛

- [[CTAN：mcmthesis](https://ctan.org/pkg/mcmthesis)](https://ctan.org/pkg/mcmthesis)
- [[GitHub：mcmthesis 源码](https://github.com/latexstudio-org/mcmthesis)](https://github.com/latexstudio-org/mcmthesis)
- [[Overleaf：MCM/ICM 模板](https://cn.overleaf.com/latex/templates/latex-template-for-mcm-icm/rwgdhsxfxkwj)](https://cn.overleaf.com/latex/templates/latex-template-for-mcm-icm/rwgdhsxfxkwj)

`mcmthesis` 是专门为 MCM/ICM 论文设计的文档类，TeX Live 通常已经包含该宏包。

### 全国大学生数学建模竞赛

- [https://www.latexstudio.net/index/details/index/mid/762.html](https://www.latexstudio.net/index/details/index/mid/762.html)
- GitHub 搜索：CUMCM LaTeX
- Overleaf 搜索：CUMCM

社区模板可能没有同步当年竞赛要求，参赛前必须对照主办方最新论文格式检查页边距、摘要页、编号和承诺书。

# 十七、效率工具

| 网站                                                   | 用途                        |
| ---------------------------------------------------- | ------------------------- |
| [[Tables Generator](https://www.tablesgenerator.com/)](https://www.tablesgenerator.com/) | 可视化生成普通表格和 `booktabs` 三线表 |
| [[Detexify](https://detexify.kirelabs.org/)](https://detexify.kirelabs.org/)           | 手写符号，识别相应 LaTeX 命令和宏包     |
| [[TikZ.net](https://tikz.net/)](https://tikz.net/)                        | 数学、物理、化学和流程图的 TikZ 源码     |
| [[TikZ.org](https://tikz.org/)](https://tikz.org/)                        | TikZ 系统教程和完整示例            |
| [[TeXample](https://texample.net/)](https://texample.net/)                    | TikZ/PGF 绘图案例库            |
| [[PGFPlots](https://pgfplots.net/)](https://pgfplots.net/)                    | 二维、三维科学曲线和数据绘图示例          |

# 十八、快捷键

## 1.通用

| 功能          | Windows/Linux    | macOS              |
| ----------- | ---------------- | ------------------ |
| 编译 LaTeX 项目 | `Ctrl + Alt + B` | `Cmd + Option + B` |
| 打开编译后的 PDF  | `Ctrl + Alt + V` | `Cmd + Option + V` |
| 源码定位到 PDF   | `Ctrl + Alt + J` | `Cmd + Option + J` |
| 清理辅助文件      | `Ctrl + Alt + C` | `Cmd + Option + C` |
| PDF 反向定位源码  | `Ctrl + 单击 PDF`  | `Cmd + 单击 PDF`     |

## 2.字体样式

| 快捷键                     | 生成命令         | 属性    | 常见用途          |
| ----------------------- | ------------ | ----- | ------------- |
| `Ctrl+M`，`Ctrl+B`       | `\mathbf{}`  | 数学粗体  | 向量、矩阵         |
| `Ctrl+M`，`Ctrl+Shift+B` | `\mathbb{}`  | 黑板粗体  | 数集、数域         |
| `Ctrl+M`，`Ctrl+C`       | `\mathcal{}` | 花体    | 集合族、函数空间、算子   |
| `Ctrl+M`，`Ctrl+R`       | `\mathrm{}`  | 直立衬线体 | 单位、算子名称、说明性下标 |
| `Ctrl+M`，`Ctrl+I`       | `\mathit{}`  | 数学斜体  | 多字母变量或斜体文本    |
| `Ctrl+M`，`Ctrl+S`       | `\mathsf{}`  | 无衬线体  | 特殊向量、矩阵或分类符号  |
| `Ctrl+M`，`Ctrl+T`       | `\mathtt{}`  | 等宽字体  | 代码、算法变量、字符串   |
## 3.LaTeX Workshop 常用代码片段

输入缩写后按 `Tab` 或从补全列表选择：

|输入|生成内容|
|---|---|
|`BEQ`|`equation` 环境|
|`BSEQ`|`equation*` 环境|
|`BAL`|`align` 环境|
|`BSAL`|`align*` 环境|
|`BGA`|`gather` 环境|
|`FBF`|`\textbf{}`|
|`FIT`|`\textit{}`|
|`MBF`|`\mathbf{}`|
|`MBB`|`\mathbb{}`|
|`MCA`|`\mathcal{}`|

LaTeX Workshop 还支持使用 `@` 前缀输入希腊字母和数学符号。

## 4.查看和修改全部快捷键

依次连续按：

```
Ctrl + K
Ctrl + S
```

然后搜索：

```
LaTeX Workshop
```

即可查看当前版本实际生效的所有快捷键；这比依赖固定列表更可靠，因为快捷键可能被其他扩展或个人配置覆盖。

![PixPin_2026-07-23_14-34-55.png](https://obsidian-image-bed-1379524953.cos.ap-guangzhou.myqcloud.com/Obsidian/PixPin_2026-07-23_14-34-55.png)


# 十九、基础Latex语法

**下面这份命令速查表已经覆盖 LaTeX 入门写作、公式、图表、引用和中文排版的核心需求。**

## 1. 最小中文文档

```latex
\documentclass[UTF8]{ctexart}

\title{论文标题}
\author{作者}
\date{\today}

\begin{document}

\maketitle
\tableofcontents

\section{引言}

这是正文。

\end{document}
```

---

## 2. 标题层级

```latex
\section{一级标题}
\subsection{二级标题}
\subsubsection{三级标题}
```

换段：源码中空一行。

强制换行：

```latex
第一行\\
第二行
```

---

## 3. 文字格式

```latex
\textbf{粗体}
\textit{斜体}
\underline{下划线}
\emph{强调}
\texttt{等宽字体}
```

字号：

```latex
{\small 小号文字}
{\large 大号文字}
{\Large 更大文字}
```

居中：

```latex
\begin{center}
居中内容
\end{center}
```

---

## 4. 列表

无序列表：

```latex
\begin{itemize}
  \item 第一项
  \item 第二项
\end{itemize}
```

有序列表：

```latex
\begin{enumerate}
  \item 第一步
  \item 第二步
\end{enumerate}
```

---

## 5. 数学公式

行内公式：

```latex
函数为 $y=x^2$。
```

独立公式：

```latex
\[
E=mc^2
\]
```

带编号公式：

```latex
\begin{equation}
  E=mc^2
  \label{eq:energy}
\end{equation}
```

引用公式：

```latex
式~\ref{eq:energy}
```

常用数学命令：

```latex
x^2              % 上标
x_i              % 下标
\frac{a}{b}      % 分数
\sqrt{x}         % 根号
\sum_{i=1}^{n}   % 求和
\prod_{i=1}^{n}  % 连乘
\int_a^b f(x)\,\mathrm{d}x
\lim_{x\to 0}
\infty
\alpha \beta \gamma
\leq \geq \neq
\approx
```

多行公式：

```latex
\begin{align}
  y &= ax+b, \\
  z &= cx+d.
\end{align}
```

导言区需要：

```latex
\usepackage{amsmath,amssymb}
```

矩阵：

```latex
\[
A=
\begin{bmatrix}
  1 & 2 \\
  3 & 4
\end{bmatrix}
\]
```

---

## 6. 图片

导言区：

```latex
\usepackage{graphicx}
```

正文：

```latex
\begin{figure}[htbp]
  \centering
  \includegraphics[width=0.7\textwidth]{figures/example.png}
  \caption{图片标题}
  \label{fig:example}
\end{figure}
```

引用：

```latex
如图~\ref{fig:example} 所示。
```

---

## 7. 表格

推荐三线表，导言区：

```latex
\usepackage{booktabs}
```

正文：

```latex
\begin{table}[htbp]
  \centering
  \caption{实验结果}
  \label{tab:result}
  \begin{tabular}{lcc}
    \toprule
    样品 & 温度 & 转化率 \\
    \midrule
    A & 300 & 82.5\% \\
    B & 350 & 91.2\% \\
    \bottomrule
  \end{tabular}
\end{table}
```

引用：

```latex
见表~\ref{tab:result}。
```

列格式：

```latex
l    % 左对齐
c    % 居中
r    % 右对齐
```

---

## 8. 超链接

导言区：

```latex
\usepackage{hyperref}
```

正文：

```latex
\url{https://example.com}

\href{https://example.com}{点击访问}
```

---

## 9. 参考文献

导言区：

```latex
\usepackage[
  backend=biber,
  style=numeric,
  sorting=none
]{biblatex}

\addbibresource{references.bib}
```

正文引用：

```latex
已有研究表明这一方法有效\cite{lamport1994}。
```

文末输出：

```latex
\printbibliography
```

`references.bib`：

```bibtex
@book{lamport1994,
  author    = {Leslie Lamport},
  title     = {LaTeX: A Document Preparation System},
  publisher = {Addison-Wesley},
  year      = {1994}
}
```

---

## 10. 特殊字符

以下字符需要转义：

```latex
\%    % 百分号
\_    % 下划线
\&    % 与符号
\$    % 美元符号
\#    % 井号
\{ \} % 花括号
```

注释：

```latex
% 这一行不会显示在文档中
```

---

## 11. 推荐导言区

```latex
\documentclass[UTF8,a4paper,12pt]{ctexart}

\usepackage{amsmath,amssymb}
\usepackage{graphicx}
\usepackage{booktabs}
\usepackage{hyperref}
\usepackage{geometry}

\geometry{
  left=2.5cm,
  right=2.5cm,
  top=2.5cm,
  bottom=2.5cm
}
```

## 12. VS Code 常用快捷键

|功能|快捷键|
|---|---|
|编译|`Ctrl + Alt + B`|
|查看 PDF|`Ctrl + Alt + V`|
|源码定位 PDF|`Ctrl + Alt + J`|
|清理辅助文件|`Ctrl + Alt + C`|
|保存|`Ctrl + S`|
|格式化|`Shift + Alt + F`|