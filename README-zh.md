# Poster Template

[English README](README.md)

这是一个可复用的 `tikzposter` 科研海报模板。内容、会议布局和机构品牌样式相互分离，方便切换主题而不重写海报。

## 快速开始

```bash
latexmk -xelatex main.tex
```

编译示例：

```bash
cd examples/icml_xiaomi_mecat
latexmk -xelatex main.tex
```

## 主要编辑位置

```text
poster-config.tex        标题、作者、主题、logo、本地覆盖
main.tex                 block 顺序、列布局和 block 高度
sections/*.tex           海报内容
assets/                  可复用 logo 和图片
themes/conference/*.tex  会议布局和左侧 logo
themes/institution/*.tex 机构颜色和右侧 logo
```

## 选择主题

在 `poster-config.tex` 中加载一个会议主题和一个机构主题：

```tex
\input{themes/conference/icml.tex}
\input{themes/institution/xiaomi.tex}
```

在 `examples/*/poster-config.tex` 中使用 `../../`：

```tex
\input{../../themes/conference/icassp.tex}
\input{../../themes/institution/xiaomi.tex}
```

白色标题栏和原色 logo 使用 `*-light.tex`。

## 标题和 Logo

设置标题信息，并挂载左右 logo：

```tex
\title{\parbox{\linewidth}{\centering Your Poster Title}}
\author{Author One\textsuperscript{1}, Author Two\textsuperscript{2}}
\institute{\textsuperscript{1}Institution One \quad \textsuperscript{2}Institution Two}
\titlegraphicleft{\PosterLeftLogo}
\titlegraphic{\PosterRightLogo}
```

在加载主题之后覆盖 logo：

```tex
\renewcommand{\PosterLeftLogo}{\includegraphics[height=7.5cm]{\PosterRootPath/assets/conferences/icml/white.png}}
\renewcommand{\PosterRightLogo}{\includegraphics[height=10cm]{\PosterRootPath/assets/institutions/xiaomi/white.png}}
```

Logo 文件使用颜色/变体命名，例如 `original.png`、`white.png`、`red.png`、`orange.png`、`orange_wordmark.svg`。

## 替换示例图片

- 会议 logo：替换 `assets/conferences/<conference>/` 下的文件，或在 `poster-config.tex` 中覆盖 `\PosterLeftLogo`。
- 机构 logo：替换 `assets/institutions/<institution>/` 下的文件，或在 `poster-config.tex` 中覆盖 `\PosterRightLogo`。
- 结构图/框架图：替换 `examples/<example>/assets/framework.png`；该图片由 `examples/<example>/sections/02-framework.tex` 引用。

## 颜色

机构主题定义颜色。可在 `poster-config.tex` 的主题加载之后覆盖：

```tex
\definecolor{SUBlue}{HTML}{FF6900}
\definecolor{highlightColor}{HTML}{FF7101}
\definecolor{PosterTitleBg}{HTML}{FF6900}
\definecolor{PosterTitleFg}{HTML}{FFFFFF}
\renewcommand{\PosterHighlightColor}{highlightColor}
```

- `SUBlue`：block/主题强调色
- `highlightColor`：`\PosterHighlight{...}` 使用的颜色
- `PosterTitleBg`：标题栏背景色
- `PosterTitleFg`：标题栏文字颜色

## 调整标题布局

调整左 logo、标题文字、右 logo 的横向空间：

```tex
\renewcommand{\PosterTitleLeftWidth}{0.16\linewidth}
\renewcommand{\PosterTitleCenterWidth}{0.62\linewidth}
\renewcommand{\PosterTitleRightWidth}{0.08\linewidth}
```

调整垂直位置：

```tex
\renewcommand{\PosterLeftLogoYOffset}{0.3cm}
\renewcommand{\PosterTitleYOffset}{-0.2cm}
\renewcommand{\PosterRightLogoYOffset}{0.3cm}
```

正值向上移动，负值向下移动。Logo 大小通过 `\includegraphics` 里的 `height=...` 调整。

## 调整 Block 两行间距

`main.tex` 负责放置 block。典型 block 写法：

```tex
\PosterInputBlock{Motivation}{\PosterRowOneHeight}{sections/01-motivation.tex}
```

两行海报中，第二行位置由第一行高度控制。在加载主题之后调整：

```tex
\renewcommand{\PosterRowOneHeight}{11.2in}
```

数值越小，第二行越靠上；数值越大，第二行越靠下。用 `\PosterRowTwoHeight` 调整第二行内部高度。

## 示例

本仓库保留上传到 GitHub 的公开示例：

- `examples/icml_xiaomi_mecat/`：ICML + Xiaomi

![ICML Xiaomi MeCAT poster](https://cdn.jsdelivr.net/gh/nyd3001/Poster-template@main/examples/icml_xiaomi_mecat/preview.jpg)

- `examples/icml_xiaomi_mecat_light/`：ICML light + Xiaomi light

![ICML Xiaomi MeCAT poster light theme](https://cdn.jsdelivr.net/gh/nyd3001/Poster-template@main/examples/icml_xiaomi_mecat_light/preview.jpg)
