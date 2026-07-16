# Poster Template

[中文文档](README-zh.md)

A reusable `tikzposter` template for research posters. Content, conference layout, and institution branding are separated so you can switch themes without rewriting the poster.

Author: Yadong Niu, MiLM Plus, Xiaomi Inc.

## Quick Start

```bash
latexmk -xelatex main.tex
```

Compile an example:

```bash
cd examples/icml_xiaomi_mecat
latexmk -xelatex main.tex
```

## What to Edit

```text
poster-config.tex        title, authors, themes, logos, local overrides
main.tex                 block order, columns, and block heights
sections/*.tex           poster content
assets/                  reusable logos and images
themes/conference/*.tex  conference layout and left logo
themes/institution/*.tex institution colors and right logo
```

## Choose Themes

In `poster-config.tex`, load one conference theme and one institution theme:

```tex
\input{themes/conference/icml.tex}
\input{themes/institution/xiaomi.tex}
```

Inside `examples/*/poster-config.tex`, use `../../`:

```tex
\input{../../themes/conference/icassp.tex}
\input{../../themes/institution/xiaomi.tex}
```

Use `*-light.tex` for white title bars with original-color logos.

## Title and Logos

Set title metadata and attach the left/right logos:

```tex
\title{\parbox{\linewidth}{\centering Your Poster Title}}
\author{Author One\textsuperscript{1}, Author Two\textsuperscript{2}}
\institute{\textsuperscript{1}Institution One \quad \textsuperscript{2}Institution Two}
\titlegraphicleft{\PosterLeftLogo}
\titlegraphic{\PosterRightLogo}
```

Override logos after loading themes:

```tex
\renewcommand{\PosterLeftLogo}{\includegraphics[height=7.5cm]{\PosterRootPath/assets/conferences/icml/white.png}}
\renewcommand{\PosterRightLogo}{\includegraphics[height=10cm]{\PosterRootPath/assets/institutions/xiaomi/white.png}}
```

Logo files use color/variant names such as `original.png`, `white.png`, `red.png`, `orange.png`, and `orange_wordmark.svg`.

## Colors

Institution themes define colors. Override them in `poster-config.tex` after theme inputs:

```tex
\definecolor{SUBlue}{HTML}{FF6900}
\definecolor{highlightColor}{HTML}{FF7101}
\definecolor{PosterTitleBg}{HTML}{FF6900}
\definecolor{PosterTitleFg}{HTML}{FFFFFF}
\renewcommand{\PosterHighlightColor}{highlightColor}
```

- `SUBlue`: block/theme accent color
- `highlightColor`: color used by `\PosterHighlight{...}`
- `PosterTitleBg`: title bar background
- `PosterTitleFg`: title bar text color

## Adjust Title Layout

Adjust horizontal space for left logo, title text, and right logo:

```tex
\renewcommand{\PosterTitleLeftWidth}{0.16\linewidth}
\renewcommand{\PosterTitleCenterWidth}{0.62\linewidth}
\renewcommand{\PosterTitleRightWidth}{0.08\linewidth}
```

Adjust vertical position:

```tex
\renewcommand{\PosterLeftLogoYOffset}{0.3cm}
\renewcommand{\PosterTitleYOffset}{-0.2cm}
\renewcommand{\PosterRightLogoYOffset}{0.3cm}
```

Positive values move upward; negative values move downward. Change logo size with `height=...` in `\includegraphics`.

## Adjust Block Rows

`main.tex` places blocks. A typical block is:

```tex
\PosterInputBlock{Motivation}{\PosterRowOneHeight}{sections/01-motivation.tex}
```

For two-row posters, move the second row by changing first-row height after loading themes:

```tex
\renewcommand{\PosterRowOneHeight}{11.2in}
```

Smaller values move the second row upward; larger values move it downward. Use `\PosterRowTwoHeight` to tune the second row's internal height.

## Examples

Public examples kept in this repository:

- `examples/icml_xiaomi_mecat/`: ICML + Xiaomi
- `examples/icml_xiaomi_mecat_light/`: ICML light + Xiaomi light
