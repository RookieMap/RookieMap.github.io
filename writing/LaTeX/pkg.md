# some useful packages for academic writing

LaTeX写作中常用到的包


## Math

* **amsmath**和**mathtools**: 数据基础包，`mathtools` 是 `amsmath` 包的扩展。
  * `amsmath` 提供了多行公式环境如`align`、`gather`，以及矩阵环境`matrix`、`pmatrix`、`bmatrix`
  * `mathtools` 提供了更多关于matrix的功能、额外的分式样式，如```splitfrac```用于分割超长分式、`mathclap`压缩空间，如有时候`sum`的条件太长，类似作用的还有`substack`用于多行条件。
  ```TeX
  \begin{equation}
  T=\sum_{
    \mathclap{\substack{i_1,\ldots,i_n=1 \\ j_1,\ldots,j_m=1}}}^d
    T_{j_1,\ldots,j_m}^{i_1,\ldots,i_n}
    E_{i_1,\ldots,i_n}^{j_1,\ldots,j_m}
    \end{equation}
  ```

* **bm**: better package for bold font in equation. 
  * 普通的mathbf并不能对希腊字母等符号正确加粗，并且对普通英文字符的加粗会改变原符号的字体，如从```italic```变为```roman```。因此，更合适的是使用```bm```或者使用```amsmath```实际上是load的```amsbsy```）中的```boldsymbol```。两者的比较可见[https://tex.stackexchange.com/questions/3238/bm-package-versus-boldsymbol](https://tex.stackexchange.com/questions/3238/bm-package-versus-boldsymbol)。一般情况在，```bm```是首选。
  * 另外需要的是```bm```包与其他一些包如```amsmath```加载顺序可能有冲突,```bm```需要在```amsmath```之后加载。有时候还会遇到```"Too many math alphabets used in version normal."```错误，可参考[https://texfaq.org/FAQ-manymathalph.html](https://texfaq.org/FAQ-manymathalph.html)
* **scalerel**: The package provides four commands for vertically scaling and stretching objects. 有时候，公式的上下标太复杂，感觉比例不协调，可以用`scalerel`强行调整。
* **siunitx**: formats numbers, quantities and units。最直接的用法是关于单位和数字的排版，如自动科学计数法，千位分隔符。此外，`siunitx`已经取代了之前的`sistyle`包。
* **amsfonts**和 **smssymb**: 提供了额外的数学符号和字体
* **thmtools**、**amsthm**、**ntheorem**: 定理环境，`amsthm`与`amsmath`兼容性更好，并且相比`ntheorem`维护更多点。
* **breqn**: facilitates automatic line-breaking of displayed math expressions。公式自动换行，但感觉还是手动靠谱点
* **xfrac**: Split-level fractions，提供`sfrac`命令，产生更好的斜分数。

## Figure

`Figure`和下面的`Table`其实都是浮动体，有一些红包的功能是通用的，如`caption`、`adjustbox`。

* **graphicx**: 包提供了插入图形的强大功能，可以处理各种图形格式，并提供了许多调整图形大小和旋转图形的选项。
```TeX
\includegraphics[options]{filename}
```
* **[caption](https://ctan.org/pkg/caption?lang=en)**: Customising captions in floating environments. 可以用来调整图中的标题，包括调整caption与浮动体之间的间距。这是一个常用的压缩论文排版的trick.
```TeX
\includegraphics[width=0.5\textwidth]{example-image}
\captionsetup{font=small,labelfont=bf,textfont=it,skip=5pt}
\caption{This is an example image}
```
这里`skip`也可以在load package的时候设置，全局生效。
* **[subcaption](https://ctan.org/pkg/subcaption?lang=en)**: supersedes caption if you use subfloats。多图还有另一个常用的包`subfig`，但一般更推荐使用`subcaption`。
```TeX
\begin{figure}
    \centering
    \begin{subfigure}[b]{0.3\textwidth}
        \includegraphics[width=\textwidth]{example-image-a}
        \caption{Image A}
    \end{subfigure}
    \begin{subfigure}[b]{0.3\textwidth}
        \includegraphics[width=\textwidth]{example-image-b}
        \caption{Image B}
    \end{subfigure}
    \caption{Two example images}
\end{figure}
```
* **[wrapfig](https://ctan.org/pkg/wrapfig?lang=en)**: Produces figures which text can flow around。可用于图文混排文字环绕等情况，一般较少用到。
* **overpic**: Combine LATEX commands over included graphics. 如果想简单地在图片上加个文字或图之类的功能（当然这可以用`Tikz`实现）
```TeX
\begin{overpic}[width=0.5\textwidth,grid,tics=10]{example-image}
    \put(50,50){\Large\textbf{Text on Image}}
\end{overpic}
```
* **[placeins](https://ctan.org/pkg/placeins?lang=en)**: Control float placement. 提供了`\FloatBarrier`命令，可以迫使LaTeX立即处理被搁置的浮动体，但并不开始一个新页（定制版的`\clearpage`）。 一个简单直接的应用是：有时候图表离文字太远，如果希望避免浮动体跨过 `\section`等章节标题，可以使用`placeins`宏包，在章节标题前，强制输出上一章节中尚未输出的浮动体。`\usepackage[section]{placeins}`


## Table
* **booktabs**: 提供了```toprule```、```bottomrule```、```midrule```、```cmidrule```等命令，可以生成效果更好的三线表
```TeX
\begin{tabular}{rl}
	\toprule
	\textbf{name} & \textbf{version} \\ 
	\midrule
	tool A & 1.0\\
	tool B & 5.3\\
	tool C & 4.0\\
	\bottomrule
\end{tabular}
```
* **multirow**: 多行表格
* **makecell**: Tabular column heads and multilined cells，可用于table中多行文本
* **colortbl**: 为表格单元格添加颜色
* **threeparttable**: 一般不会用到，但是如果想在表格中加上footnote的话，
```TeX
\begin{table}
\centering
\caption{This is a table with a footnote.}
\begin{threeparttable}
\begin{tabular}{c c}
\toprule
A & B \\
\midrule
1 & 2 \\
3 & 4 \\
\bottomrule
\end{tabular}
\begin{tablenotes}
\item[\tnote{1}] This is a footnote.
\end{tablenotes}
\end{threeparttable}
\end{table}
```
* **[tabularray](https://ctan.org/pkg/tabularray?lang=en)**: Typeset tabulars and arrays with LATEX3，一个新的非常强大的table工具包，几乎能实现其他包提供的所有功能。
  * 更简洁的语法：tabularray 允许使用简洁的语法来定义列和行的格式。
  * 灵活的列和行格式：你可以轻松地指定列和行的宽度、高度和对齐方式。
  * 更好的垂直对齐：tabularray 自动处理单元格的垂直对齐，并允许使用多种选项进行调整。
  * 颜色和样式：可以方便地为单元格、行和列添加背景颜色和边框样式。
* **adjustbox**: Graphics package-alike macros for “general” boxes, e.g. minipage. `adjustbox` 包提供了调整盒子（包括图像）的各种工具，例如裁剪、缩放和旋转。最常用的场景，防止table超边界。
```TeX
\begin{adjustbox}{width=0.5\textwidth,clip,trim=0cm 1cm 0cm 1cm}
    \includegraphics{example-image}
\end{adjustbox}
\begin{adjustbox}{max width=\textwidth}
    \begin{tabular}{ c c c c c}
        \toprule
        Header 1 & Header 2 & Header 3 & Header 4 & Header 5  \\
        \midrule
        Data 1 & Data 2 & Data 3 & Data 4 & Data 5 \\
        \bottomrule
    \end{tabular}
\end{adjustbox}
```

## Itemize
* **[enumitem](https://ctan.org/pkg/enumitem?lang=en)**: 可能是最流行的用于定制列表的包，可以定制缩进、间距，在压缩版面时候经常派上用场。另一个常用的场景是行内list，也就是正文中的list环境。
```tex
\begin{itemize}[label=$\star$, leftmargin=2cm]
   \item Item 1
   \item Item 2
\end{itemize}
```

## Color
* **xcolor**: 最常用的颜色包之一，提供了易于使用的接口来选择和定义颜色。
  * 它支持多种颜色模型（如 RGB, CMY, CMYK 等）。
  * 可以定义自己的颜色和混合颜色（如`red!50!green!20!blue`）。
```tex
\usepackage{xcolor}
\definecolor{tea_green}{RGB}{214, 234, 193}
\definecolor{mygreen}{rgb}{0, 0.6, 0}
\textcolor{mygreen}{This text is in my custom green color.}
\textcolor[cmy]{0.7,0.5,0.3}{foo}
```

## Algorithm/Code
### 伪代码
* **algorithm**: float wrapper for algorithms.
  * `algorithm` 包主要提供了一个浮动环境，叫做 `algorithm` 环境。这个环境可以让你把算法当作一个图或表一样的浮动对象来处理，这样它可以自动地排版到合适的位置。
  * 它不包含用于排版伪代码的命令，通常与 `algorithmic` 或 `algorithmicx` 配合使用。

<!-- * **algorithmic**: first algorithm typesetting environment. -->
* **[algorithmicx](https://ctan.org/pkg/algorithmicx?lang=en)**: 可以看作是`algorithmic`的升级版，更多定制选项等，用于排版伪代码。官方文档abs如下：
> The algorithmicx package provides many possibilities to customize the layout of algorithms. You can use one of the predefined layouts (pseudocode, pascal and c and others), with or without modifications, or you can define a completely new layout for your specific needs.
* **algpseudocode**:  是 `algorithmicx` 包的一个样式，当加载 `algpseudocode` 包时，它会配置 `algorithmicx` 的样式，使伪代码看起来像传统的算法伪代码。类似的还有`pascal`、`c`等样式。另外，还有一个更新的包[`algpseudocodex`](https://ctan.org/pkg/algpseudocodex?lang=en)
>  It is based on algpseudocode from the algorithmicx package and uses the same syntax, but adds several new features and improvements. Notable features include customizable indent guide lines and the ability to draw boxes around parts of the code for highlighting differences.
* **[algorithm2e](https://ctan.org/pkg/algorithm2e?lang=en)**: 是另一个类似于`algorithmicx`的包: “Floating algorithm environment with algorithmic keywords”. 提供了不同的语法和定制选项。语法更简单，样式定制更多。

<!-- ToDo：给出不同的样例图？ -->

### 代码
* **[listings](https://ctan.org/pkg/listings?lang=en)**: 排版源码最常用的基础包之一 

```tex
\usepackage{listings}
\usepackage{xcolor}
\lstset{
    basicstyle=\ttfamily,
    keywordstyle=\color{blue},
    commentstyle=\color{green},
    numbers=left,
}

\begin{lstlisting}[language=Python]
# This is a comment
def function(x):
    return x + 1
\end{lstlisting}
```

* **[minted](https://ctan.org/pkg/minted?lang=en)**: a LaTeX package that facilitates expressive syntax highlighting using the Pygments library. 提供了非常多的语言支持和更漂亮的默认样式。需要使用 -shell-escape 选项编译 LaTeX 文档，因为它依赖于外部工具，但也可以设置使用`fancyvrb`输出。 https://github.com/gpoore/minted 
* **[pythontex](https://github.com/gpoore/pythontex)**: 这个包和`minted`包是一个作者，可以用于在LaTeX中执行python代码并展示结果，也可以高亮code。可以用在数据可视化、动态计算结果、自动化报告场景。


## Ref
* **backref**: \usepackage[hyperpageref]{backref} % add backlinks from the references to the cited pages
* **cleveref**: \cref, \Cref command for table, figure
* \usepackage{hyperref} % should be imported after all other packages as it changes a lot


## Drawing

* [tikzsymbols](https://ctan.org/pkg/tikzsymbols?lang=en)
* [tikzpeople](https://ctan.org/pkg/tikzpeople?lang=en)

* [fontawesome](https://www.ctan.org/pkg/fontawesome)
  * The package offers access to the large number of web-related icons provided by the included font.
* [tikz-network](https://ctan.org/pkg/tikz-network?lang=en)
  * This package allows the creation of images of complex networks that are seamlessly integrated into the underlying LaTeX files.
* [tikzducks](https://www.ctan.org/pkg/tikzducks) 各种小鸭子
* [tikzmarmots](https://www.ctan.org/pkg/tikzmarmots) 各种土拨鼠
* [TikZlings](https://ctan.org/pkg/tikzlings?lang=en) 更全的小动物 A collection of LATEX packages for drawing cute little animals and similar creatures using TikZ.

### Tikz/PGF



example gallery
* [tikz_favorites gitbhu](https://f0nzie.github.io/tikz_favorites/)
* 

* https://github.com/nschloe/tikzplotlib


`tcolorbox`
`fancyvrb`

## Review

* [changes](https://ctan.org/pkg/changes?lang=en): LaTeX 标注宏包，实现highlights, additions, deletions, or replacements等标记操作，具体可看文档，可以设置修改者标识。可用于跟踪文档的更改和修订，特别是在合作项目中，可以生成更改的摘要列表，方便查看所有的更改和修订。
```tex
\usepackage[commandnameprefix=ifneeded, todonotes={textsize=tiny}]{changes} %commentmarkup=margin
\usepackage{changes} %final
\usepackage{CJKutf8}

\definechangesauthor[name={Fei}, color=red]{Fei} %修订作者1
\newcommand{\margincomm}[2]{\highlight[id=Fei, comment={\begin{CJK*}{UTF8}{gkai}#2\end{CJK*}}]{#1}}
```

* [pdfcomment](https://ctan.org/pkg/pdfcomment?lang=en): A user-friendly interface to pdf annotations, 主要侧重于实现各种comments形式，提供了许多选项来自定义注释的外观和行为，需要注意主要针对Adobe Reader开发，不同的reader软件，看到的效果可能有差异。
```tex
\usepackage{pdfcomment}
\defineavatar{SF}{icon=Comment, color=red, author={Fei Sun}}

\newcommand\feicomm[1]{\pdfcomment[avatar=SF]{\begin{CJK*}{UTF8}{gkai}#1\end{CJK*}}}
\newcommand\hlcomm[2]{\pdfmarkupcomment[avatar=SF, markup=Highlight, color=yellow]{#1}{\begin{CJK*}{UTF8}{gkai}#2\end{CJK*}}}
```

* [latexdiff](https://ctan.org/pkg/latexdiff?lang=en): 一个用于比较两个LaTeX文件之间差异的命令行工具，编译为pdf文件，在修订过程中突出显示文档中的更改。这对于合作项目、学术写作、论文修订等场景特别有用。
  


## Misc
* **soul**: ```\setstcolor{red}```
* **babel**: ```\usepackage[english]{babel}```
* **todonotes**: 
* **marginnote**:
* **acronym**:
```TeX
\usepackage[printonlyused,withpage]{acronym}

\begin{acronym}
  \acro{API}{Application Programming Interface}
\end{acronym}

% usage in text
\ac{API} % API, show full if first use
\acf{API} % always Application Programming Interface (API)
\acp{API} % APIs, show full if first use
\acfp{API} % always Application Programming Interfaces (APIs)
\acs{API} % always API
```
