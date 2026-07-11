# LaTeX A4 中文公文模板


正文及各级标题中的：

- 英文字母；
- 英文单词；
- 阿拉伯数字；
- 英文标点；

统一使用 **Times New Roman**。

中文仍按原模板设置：

- 主标题：方正小标宋简体；
- 一级标题：黑体；
- 二级标题：楷体_GB2312；
- 三级标题：仿宋_GB2312；
- 正文：仿宋_GB2312。

模板中的西文字体设置为：

```latex
\IfFontExistsTF{Times New Roman}{
  \setmainfont[
    Ligatures=TeX
  ]{Times New Roman}
}{
  \setmainfont[
    Ligatures=TeX
  ]{TeX Gyre Termes}
}
```

系统已安装 Times New Roman 时，会直接调用 Times New Roman。未安装时，自动使用 TeX Gyre Termes，以避免编译失败。

## 可选目录

在 `\begin{document}` 后加入：

```latex
\MakeOfficialTOC
```

即可生成目录。不加入该命令时，不生成目录。

## 页码

默认页码格式：

```text
— 1 —
```

- 奇数页：正文版心右侧；
- 偶数页：正文版心左侧；
- 字号：四号，14 pt；
- 页码数字使用 Times New Roman；
- 两侧破折号保持中文全角破折号样式。

## 编译

必须使用 XeLaTeX：

```bash
xelatex main.tex
xelatex main.tex
```

或：

```bash
latexmk main.tex
```
