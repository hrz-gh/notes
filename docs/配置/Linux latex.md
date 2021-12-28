# Linux latex 配置

## 安装texlive

[清华大学开源软件镜像站](https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/Images/)

```bash
sudo apt-get install perl-tk
sudo mount -o loop texlive* /mnt
cd /mnt
./install-tl -gui
echo "# TeXLive2019-path

export PATH=/usr/local/texlive/2019/bin/x86_64-linux:$PATH
export MANPATH=/usr/local/texlive/2019/texmf-dist/doc/man:$MANPATH
export INFOPATH=/usr/local/texlive/2019/texmf-dist/doc/info:$INFOPATH" >> ~/.bashrc
cd ..
sudo umount /mnt
```

## 配置vscode

安装LaTeX Workshop插件

```json
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

## 字体

中文可直接使用，默认是fandol，但会有wannring，可以忽略。

实在不想有wannring，可安装windows字体，[参考1](https://blog.csdn.net/Candylx/article/details/111999699)，再使用:

```tex
\documentclass[fontset=windows]{ctexart}
```