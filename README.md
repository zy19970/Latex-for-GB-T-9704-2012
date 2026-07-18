# GB/T 9704—2012 党政机关公文 XeLaTeX 模板使用说明

本项目提供一份基于 **GB/T 9704—2012《党政机关公文格式》**编排参数制作的 XeLaTeX 模板，适用于通知、请示、报告、函等常见党政机关公文的排版。

> 模板用于辅助排版。正式印发前，仍应结合发文机关的具体规定、印章位置、签发流程、版记内容及实际印刷效果进行复核。

---

## 1. 模板主要特性

模板当前包含以下功能：

- A4 纸张，版心约为 156 mm × 225 mm；
- 天头 37 mm，订口 28 mm；
- 正文三号仿宋，首行缩进两个汉字；
- 数字和西文字母默认使用 Times New Roman；
- 一级标题为三号黑体；
- 二级标题为三号楷体；
- 三级、四级标题为三号仿宋；
- 公文标题使用二号小标宋；
- 可选份号、密级和保密期限、紧急程度；
- 可选发文机关标志、发文字号、签发人和红色分隔线；
- 公文标题与主送机关可在不显示版头时继续保留；
- 支持附件说明、机关署名、成文日期、附注和版记；
- 支持单、双页页码位置切换；
- 支持可选目录，正文页码可从第 1 页重新开始；
- Windows 公文字体缺失时，可自动回退至开源字体以保证编译。

---

## 2. 编译环境

### 2.1 推荐编译器

必须使用：

```text
XeLaTeX
```

不要使用 `pdfLaTeX` 编译，因为模板依赖 `fontspec` 和 `xeCJK`。

### 2.2 推荐 TeX 发行版

Windows 可使用：

- TeX Live；
- MiKTeX。

macOS 可使用 MacTeX，Linux 可使用 TeX Live。

### 2.3 命令行编译

在模板所在目录执行：

```bash
xelatex GB_T_9704_2012_Official_Document_Template_v7.tex
```

通常建议连续编译两次：

```bash
xelatex GB_T_9704_2012_Official_Document_Template_v7.tex
xelatex GB_T_9704_2012_Official_Document_Template_v7.tex
```

使用目录时必须至少编译两次，才能正确生成目录及页码。

---

## 3. 字体要求

### 3.1 推荐字体

为获得更接近正式公文的排版效果，Windows 系统建议安装以下字体：

| 用途 | 推荐字体 |
|---|---|
| 公文标题 | 方正小标宋简体或 FZXiaoBiaoSong-B05S |
| 正文 | 仿宋_GB2312 |
| 一级标题 | 黑体或 SimHei |
| 二级标题 | 楷体_GB2312 |
| 页码、版记 | 宋体或 SimSun |
| 数字和西文字母 | Times New Roman |

### 3.2 字体回退

如果系统没有安装上述字体，模板会自动回退至 Noto Serif CJK SC、Noto Sans CJK SC、Tinos 等字体。

回退字体可以保证模板正常编译，但字面宽度、笔画和行距可能与正式公文字体存在差异。正式文件建议在安装规范字体的 Windows 环境中编译。

### 3.3 在 Release 中下载字体

本模板所使用的字体可在项目的 **Releases（发行版）** 页面下载。进入对应版本的 Release 后，在“Assets”或“附件”区域下载字体资源包并解压安装。

字体资源包包括模板优先调用或用于兼容回退的中文字体与西文字体。安装完成后，应关闭并重新打开 TeX 编辑器、命令行窗口或集成开发环境，再使用 XeLaTeX 重新编译。

Windows 中可选中字体文件，右键选择“安装”或“为所有用户安装”。当同一字体存在多个版本时，建议保留模板 Release 中提供或说明的版本，以减少字体名称不一致、字宽变化和版面错位。

> 字体应按照其各自的授权许可使用。若 Release 中采用来源链接或安装说明代替部分字体文件，请从所列官方或授权渠道获取。

---

## 4. 快速开始

打开模板，在“用户信息区”修改公文信息：

```tex
\DocCopyNo{}                         % 份号
\DocSecret{}                         % 密级和保密期限
% \DocSecretPeriod{机密}{1年}         % 推荐写法
\DocUrgency{}                        % 紧急程度
\DocAuthority{××市人民政府文件}       % 发文机关标志
\DocNumber{×政发〔2026〕1号}          % 发文字号
\DocSigner{}                         % 签发人
\DocTitle{关于进一步规范党政机关公文格式的通知}
\DocRecipient{各区人民政府，市政府各部门，各有关单位}
\DocAgency{××市人民政府}
\DocDate{2026年7月18日}
```

然后在正文区修改内容：

```tex
\begin{document}

% \MakeOfficialTOC
% \MakeOfficialFrontMatter

\MakeOfficialTitleBlock

这里填写正文内容。

\end{document}
```

---

## 5. 版头控制

### 5.1 显示版头

需要显示份号、密级、紧急程度、发文机关标志、发文字号及红色分隔线时，启用：

```tex
\MakeOfficialFrontMatter
```

示例：

```tex
\begin{document}

\MakeOfficialFrontMatter
\MakeOfficialTitleBlock

正文内容。

\end{document}
```

### 5.2 隐藏版头

不需要版头时，将其注释：

```tex
% \MakeOfficialFrontMatter
```

标题和主送机关仍可通过下列命令正常显示：

```tex
\MakeOfficialTitleBlock
```

### 5.3 重要逻辑

`\MakeOfficialFrontMatter` 只控制：

- 份号；
- 密级和保密期限；
- 紧急程度；
- 发文机关标志；
- 发文字号；
- 签发人；
- 红色分隔线。

`\MakeOfficialTitleBlock` 独立控制：

- 公文标题；
- 主送机关。

因此，建议始终保留：

```tex
\MakeOfficialTitleBlock
```

---

## 6. 份号、密级和紧急程度

### 6.1 份号

```tex
\DocCopyNo{000001}
```

一般使用 6 位阿拉伯数字，例如：

```text
000001
```

不需要份号时留空：

```tex
\DocCopyNo{}
```

### 6.2 密级和保密期限

推荐使用：

```tex
\DocSecretPeriod{机密}{1年}
```

输出效果：

```text
机密★1年
```

也可以自行填写：

```tex
\DocSecret{秘密★5年}
```

不需要时留空：

```tex
\DocSecret{}
```

不要同时启用 `\DocSecret` 和 `\DocSecretPeriod`。后执行的命令会覆盖前一个命令的内容。

### 6.3 紧急程度

```tex
\DocUrgency{特急}
```

或：

```tex
\DocUrgency{加急}
```

不需要时留空：

```tex
\DocUrgency{}
```

未填写的版头要素不会额外占据空行。

---

## 7. 发文机关标志、发文字号和签发人

### 7.1 发文机关标志

```tex
\DocAuthority{××市人民政府文件}
```

### 7.2 发文字号

```tex
\DocNumber{×政发〔2026〕1号}
```

注意使用六角括号：

```text
〔 〕
```

不要使用普通方括号：

```text
[ ]
```

### 7.3 签发人

普通下行文一般留空：

```tex
\DocSigner{}
```

需要签发人时填写：

```tex
\DocSigner{张三}
```

填写签发人后，发文字号和签发人会分列排版。

---

## 8. 公文标题和主送机关

### 8.1 标题

```tex
\DocTitle{关于进一步规范党政机关公文格式的通知}
```

标题由：

```tex
\MakeOfficialTitleBlock
```

输出。

### 8.2 主送机关

```tex
\DocRecipient{各区人民政府，市政府各部门，各有关单位}
```

模板会自动在末尾添加中文冒号：

```text
：
```

因此，填写时不要重复输入冒号。

不需要主送机关时：

```tex
\DocRecipient{}
```

---

## 9. 正文与标题层级

### 9.1 正文

直接输入自然段即可：

```tex
为进一步规范党政机关公文排版，提高公文处理工作的规范化、标准化水平，现就有关事项通知如下。
```

模板默认：

- 正文三号仿宋；
- 首行缩进两个汉字；
- 回行顶格；
- 段前、段后不额外增加空白。

不要在每个自然段前手动添加全角空格。

### 9.2 一级标题

```tex
\section{总体要求}
```

输出：

```text
一、总体要求
```

### 9.3 二级标题

```tex
\subsection{页面设置}
```

输出：

```text
（一）页面设置
```

### 9.4 三级标题

```tex
\subsubsection{字体字号}
```

输出：

```text
1. 字体字号
```

### 9.5 四级标题

```tex
\OfficialFourth{页码格式}
```

输出：

```text
（1）页码格式
```

标题后的首个正文自然段仍会自动首行缩进两个汉字。

---

## 10. 附件说明

### 10.1 多个附件

推荐使用结构化写法：

```tex
\begin{OfficialAttachmentList}
  \OfficialAttachmentItem{公文格式检查表}
  \OfficialAttachmentItem{公文排版常见问题说明}
\end{OfficialAttachmentList}
```

输出形式：

```text
  附件：1. 公文格式检查表
        2. 公文排版常见问题说明
```

特点：

- “附件：”左空两个汉字；
- 第一项与“附件：”处于同一基线；
- 多个附件序号纵向对齐；
- 附件名称首字纵向对齐；
- 附件名称过长时，回行与名称首字对齐。

### 10.2 单个附件

```tex
\OfficialAttachment{公文格式检查表}
```

### 10.3 旧式兼容写法

```tex
\OfficialAttachments{1. 公文格式检查表\\
2. 公文排版常见问题说明}
```

旧式写法适合内容较短的附件说明。需要自动换行时，应优先使用 `OfficialAttachmentList` 环境。

### 10.4 两位数附件序号

模板当前附件序号占位宽度为 `1.25em`，适合 1—9 个附件。如果附件达到 10 个及以上，可在模板中找到：

```tex
\makebox[1.25em][l]{\arabic{officialattachment}.}%
```

改为：

```tex
\makebox[1.75em][l]{\arabic{officialattachment}.}%
```

并相应检查附件名称的横向起始位置。

---

## 11. 发文机关署名和成文日期

先设置：

```tex
\DocAgency{××市人民政府}
\DocDate{2026年7月18日}
```

在正文末尾调用：

```tex
\MakeOfficialSignature
```

模板会将机关署名和成文日期编排在正文右侧区域。

涉及加盖印章、联合行文或特殊落款位置时，应根据实际公文类型进一步调整。

---

## 12. 附注

使用：

```tex
\OfficialNote{此件公开发布}
```

模板会自动添加中文圆括号：

```text
（此件公开发布）
```

因此，参数中不要重复输入括号。

无附注时，删除或注释该命令。

---

## 13. 版记

调用格式：

```tex
\MakeOfficialImprint{抄送机关}{印发机关}{印发日期}
```

示例：

```tex
\MakeOfficialImprint
  {各有关单位}
  {××市人民政府办公室}
  {2026年7月18日印发}
```

不需要抄送行时，第一个参数留空：

```tex
\MakeOfficialImprint
  {}
  {××市人民政府办公室}
  {2026年7月18日印发}
```

版记会自动置于页面底部，并绘制分隔线。

---

## 14. 附件首页

使用：

```tex
\MakeOfficialAttachmentTitle{1}{公文格式检查表}
```

其中：

- 第一个参数为附件序号；
- 第二个参数为附件标题。

示例：

```tex
\MakeOfficialAttachmentTitle{1}{公文格式检查表}

这里填写附件正文。
```

该命令会自动另起一页。

---

## 15. 目录功能

### 15.1 启用目录

取消注释：

```tex
\MakeOfficialTOC
```

推荐位置：

```tex
\begin{document}

\MakeOfficialTOC
\MakeOfficialFrontMatter
\MakeOfficialTitleBlock

正文内容。

\end{document}
```

目录页：

- 不显示页码；
- 不计入正文页码；
- 正文重新从第 1 页开始编号。

### 15.2 不使用目录

保持注释：

```tex
% \MakeOfficialTOC
```

### 15.3 编译次数

启用目录后，至少连续编译两次：

```bash
xelatex GB_T_9704_2012_Official_Document_Template_v7.tex
xelatex GB_T_9704_2012_Official_Document_Template_v7.tex
```

---

## 16. 页码

模板默认页码形式：

```text
— 1 —
```

当前设置：

- 四号宋体半角阿拉伯数字；
- 数字左右各有一条一字线；
- 一字线与数字保持水平视觉对齐；
- 奇数页页码位于版心右侧并右空一字；
- 偶数页页码位于版心左侧并左空一字；
- 页眉为空。

临时隐藏页码：

```tex
\HidePageNumber
```

恢复页码：

```tex
\ShowPageNumber
```

---

## 17. 完整示例

```tex
\DocCopyNo{000001}
\DocSecretPeriod{机密}{1年}
\DocUrgency{特急}
\DocAuthority{××市人民政府文件}
\DocNumber{×政发〔2026〕1号}
\DocSigner{}
\DocTitle{关于进一步规范党政机关公文格式的通知}
\DocRecipient{各区人民政府，市政府各部门，各有关单位}
\DocAgency{××市人民政府}
\DocDate{2026年7月18日}

\begin{document}

% 需要目录时启用
% \MakeOfficialTOC

% 需要版头时启用
\MakeOfficialFrontMatter

% 标题和主送机关始终保留
\MakeOfficialTitleBlock

为进一步规范党政机关公文排版，提高公文处理工作的规范化、标准化水平，现就有关事项通知如下。

\section{总体要求}
公文排版应当做到版面整洁、结构清晰、字体规范、要素完整。

\subsection{页面设置}
公文用纸采用 A4 型纸，版心尺寸为 156~mm×225~mm。

\subsubsection{字体字号}
正文一般使用三号仿宋体字。

\OfficialFourth{页码格式}
页码使用四号半角宋体阿拉伯数字。

\begin{OfficialAttachmentList}
  \OfficialAttachmentItem{公文格式检查表}
  \OfficialAttachmentItem{公文排版常见问题说明}
\end{OfficialAttachmentList}

\MakeOfficialSignature

\OfficialNote{此件公开发布}

\MakeOfficialImprint
  {各有关单位}
  {××市人民政府办公室}
  {2026年7月18日印发}

\end{document}
```

---

## 18. 常见问题

### 18.1 编译时报字体不存在

原因通常是系统未安装模板中优先调用的公文字体。

处理方法：

1. 在项目 Releases 页面的“Assets”或“附件”区域下载字体资源包；
2. 安装仿宋_GB2312、楷体_GB2312、方正小标宋简体等模板所需字体；
3. 重新启动编辑器或命令行窗口；
4. 再次使用 XeLaTeX 编译。

模板具有字体回退机制，因此多数情况下仍能编译，但排版效果可能不同。

### 18.2 星号显示为方框

不要手动直接输入不受当前字体支持的星号。推荐使用：

```tex
\DocSecretPeriod{机密}{1年}
```

模板会调用 `\OfficialSecretStar` 输出黑色实心五角星。

### 18.3 标题显示但版头不显示

这是模板的正常设计。检查是否注释了：

```tex
% \MakeOfficialFrontMatter
```

标题由下列命令独立控制：

```tex
\MakeOfficialTitleBlock
```

### 18.4 标题后的正文没有缩进

正文应以普通自然段形式输入，不要使用 `\\` 强制换行代替分段，也不要在标题后添加 `\noindent`。

正确写法：

```tex
\section{总体要求}
这里是正文自然段。
```

### 18.5 附件名称与序号之间过宽

当前 v7 已将序号占位缩小为 `1.25em`。若仍需微调，可修改：

```tex
\makebox[1.25em][l]{\arabic{officialattachment}.}%
```

数值越小，序号与名称之间越紧；数值过小可能导致两位数序号重叠。

### 18.6 数字未使用 Times New Roman

正文数字和西文字母由 `\setmainfont` 控制。检查系统是否安装 Times New Roman。未安装时会回退至 Tinos。

份号、密级期限中的数字会按三号黑体要素处理，不使用正文 Times New Roman；页码数字使用宋体字形。

### 18.7 页码位置不正确

先确认：

- 文档类仍保留 `twoside`；
- `geometry` 中左右边距没有被修改；
- 未被其他页眉页脚宏包覆盖；
- 没有重新定义 `official` 页面样式。

打印时应关闭“适合页面”“缩放到可打印区域”等选项，使用 100% 原始尺寸打印。

### 18.8 目录页码不更新

连续编译两次或三次，删除旧的 `.aux`、`.toc` 文件后重新编译。

---

## 19. 不建议随意修改的参数

除非明确了解公文版式和 LaTeX 页面模型，否则不建议随意修改：

```tex
top=37mm
bottom=35mm
left=28mm
right=26mm
footskip=7mm
```

也不建议直接修改：

- `\OfficialBodyFont`；
- `\OfficialTitleFont`；
- `\OfficialPageNumber`；
- `\fancypagestyle{official}`；
- `\MakeOfficialFrontMatter`；
- 附件列表的横向宽度计算。

修改这些内容可能导致版心、行距、页码或附件说明错位。

---

## 20. 文件组织建议

可以将模板复制为具体公文文件：

```text
project/
├─ official-document.tex
├─ README_GB_T_9704_2012_Template.md
├─ figures/
└─ attachments/
```

建议不要直接在唯一的原始模板上长期编辑，而是保留一份未修改的模板作为备份。

---

## 21. 版本说明


v7 的主要调整包括：

- 公文标题与可选版头分离；
- 修正正文首行缩进；
- 修正页码一字线与数字的水平视觉对齐；
- 修正奇偶页页码定位；
- 修正份号、密级和紧急程度的字体与排列顺序；
- 优化附件说明中序号与附件名称的横向间距；
- 保留多附件自动换行和纵向对齐功能。
