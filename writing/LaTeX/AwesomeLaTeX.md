# Awesome LaTeX

Author: [@FeiSun](https://github.com/FeiSun)

> This is a curated list of awesome stuff for the [(La)TeX typesetting system](https://www.latex-project.org/).

## Distributions

- [MacTeX](https://tug.org/mactex/) - mac平台下常用的LaTeX发行版 
- [TeX Live](https://www.tug.org/texlive/) - Most common LaTeX distribution for Unix-like operating systems, including GNU/Linux. Also works on Windows. 
- [MikTeX](https://miktex.org) - Most common LaTeX distribution for Windows, but also available for Mac, Linux or as Docker image.

## Engines
**最常用的为 pdf(La)TeX和Xe(La)TeX**

- [pdfTeX](https://www.tug.org/applications/pdftex/) - TeX compiler that produces PDF files immediately instead of DVI files (nowadays, this is the standard compiler for many users).
- [XeTeX](http://xetex.sourceforge.net) - TeX compiler that provides better unicode and font support than TeX/pdfTeX (i.e. you can use the  fonts of your operating system instead of only TeX fonts).
- [LuaTeX](https://www.luatex.org) - (La)TeX compiler that supports Lua code for scripting and has improved unicode and font support than standard TeX/pdfTeX.
- [tectonic](https://tectonic-typesetting.GitHub.io/en-US/) - Modern, self contained (La)TeX compiler powered by XeTeX and TeXLive.

## Editors

- [List of popular LaTeX editors](https://tex.stackexchange.com/questions/339/latex-editors-ides) - Community-maintained list of popular LaTeX editors including a screenshot and a short description.

### LaTeX-focused

Some of the most awesome editor for LaTeX do just that: edit LaTeX.

- [Texpad/texifier](https://www.texpad.com) - Commercial LaTeX editor for macOS and iOS, with excellent features (document overview, synchronised PDF display, autocompletion, sync across devices, etc.) that never get in the way of writing.
- [TeXMaker](https://www.xm1math.net/texmaker/) - Pretty good alternative to Kile.
- [TeXStudio](https://www.texstudio.org) - Cross-platform LaTeX editor that stems from TeXMaker.
- [WinEdt](https://www.winedt.com) - The LaTeX editor many people swear by. Only for windows.
- [LyX](https://www.lyx.org) - Cross-platform WYSIWYM editor that uses LaTeX behind the scenes to render documents. 
- [TeXShop](https://pages.uoregon.edu/koch/texshop/) - No-nonsense editor for LaTeX documents which is included in MacTeX. 
- [TeXWorks](https://www.tug.org/texworks/) - No-nonsense editor for LaTeX code, modeled after TeXShop, but this one is cross-platform. 

### General purpose text editors

These editors are no one-trick ponies: sure, they edit LaTeX, but they can do a lot more!

- [VS Code](https://code.visualstudio.com/) [[awesome resource]](https://github.com/viatsko/awesome-vscode) **首推**
  - [LaTeX Workshop](https://github.com/James-Yu/LaTeX-Workshop) - LaTeX extension for Visual Studio Code
  - [LTeX](https://marketplace.visualstudio.com/items?itemName=valentjn.vscode-ltex) - LanguageTool grammar/spell checking

- [Emacs](https://www.gnu.org/software/emacs/)  [[awesome resource]](https://github.com/emacs-tw/awesome-emacs)
  - [AucTeX](https://www.gnu.org/software/auctex/) - Emacs plugin for LaTeX that also shows a preview of equations and figures.
  - [RefTeX](https://www.gnu.org/software/auctex/reftex) - Emacs plugin for LaTeX that adds support for labels, references, and citations.

- [Vim](https://www.vim.org) [[awesome resource]](https://github.com/mhinz/vim-galore)
  - [Vim-LaTeX](http://vim-latex.sourceforge.net)
  - [LaTeX Live Preview](https://github.com/xuhdev/vim-latex-live-preview) - Instantly previews your LaTeX document.
  - [vimtex](https://github.com/lervag/vimtex) - Modern vim plugin for editing LaTeX files. Has a variety of features including live preview and forward search.

- [Atom](https://atom.io) [[awesome resource]](https://github.com/mehcode/awesome-atom)
  - [LaTeXTools](https://atom.io/packages/latextools) - Atom port of the Sublime Text package of the same name.

- [Sublime Text](https://www.sublimetext.com) [[awesome resource]](https://github.com/dreikanter/sublime-bookmarks)
  - [LaTeXing](https://github.com/LaTeXing/LaTeXing) - Free plug-in to edit LaTeX.
  - [LaTeXTools](https://github.com/SublimeText/LaTeXTools) - Free LaTeX plugin for Sublime Text.

### Online editors

Online editors that allow you to edit documents collaboratively.

- [List of popular online LaTeX editors](https://tex.stackexchange.com/questions/3/compiling-documents-online/1654#1654) - Community-maintained list of popular online LaTeX editor including equation editors.
- [Overleaf](https://www.overleaf.com) - Online editor, also with a WYSIWYM editor and git support.

## Bibliography tools

- [Zotero](https://www.zotero.org) - Reference manager for your browser that also exports to bibtex and integrates with many LaTeX editors. 
- [Paperpile](https://paperpile.com) - A web-based commercial reference management software, with special emphasis on integration with Google Docs and Google Scholar.
- [Mendeley](https://www.mendeley.com) - Both an app and cloud client to manage your references and PDFs. Can sync out to a bibtex file for your LaTeX workflow. 
- [Papis](https://github.com/papis/papis) - Extremely customizable, powerful and simple cross-platform (Python) library manager. It has a very complete Command-Line-Interface, several GUIs and scripting capability.
- [JabRef](https://www.jabref.org) - Very powerful cross-platform (Java) bibtex editor. 
- [betterbib](https://github.com/nschloe/betterbib) - Command-line utility for improving your BibTeX files. Fetches information from online sources. 

## Build Tools

Compiling LaTeX documents can be tedious, build tools help you to manage the compilation process.

- [Arara](https://www.ctan.org/pkg/arara) ([GitHub repo](https://github.com/islandoftex/arara)) - Simple tool that allows you to specify which tools to call inside your document and it can be extended quite easily. 
- [latexmk](https://www.ctan.org/pkg/latexmk) - Build tool that is the commonly used by many LaTeX editors (LaTeXing, TeXShop, etc.) to build your LaTeX files. 


## Misc. Tools

- [Pandoc](https://pandoc.org) - This program converts almost any document format (LaTeX, DOC, markdown, etc.) to almost any other format. A great tool to aid workflows where multiple formats are used. 


## Slides

* [Beamer](https://ctan.org/pkg/beamer?lang=en) A LATEX class for producing presentations and slides.
  * [beamer theme gallery](https://deic.uab.cat/~iblanes/beamer_gallery/)
  * 比较推荐 [Metropolis](https://github.com/matze/mtheme) ([ctan link](https://ctan.org/pkg/beamertheme-metropolis?lang=en)) 主题

## Poster 学术海报

* [Better Poster Latex Template](https://github.com/rafaelbailo/betterposter-latex-template) LaTeX Template for Mike Morrison's betterposter
* [better_poster_latex](https://github.com/LanaSina/better_poster_latex) The Latex version of Mike Morrison's "better poster" template
* [Better Scientific Poster](https://osf.io/ef53g/) ppt version
* [tikzposter](https://www.ctan.org/pkg/tikzposter) 
* [beamerposter](https://ctan.org/pkg/beamerposter?lang=en)
* [Research Design (R&D) Poster Presentation](https://github.com/SuperBruceJia/Poster_Template)

## LaTeX book/tutorial
* [The TeXBook](https://visualmatheditor.equatheque.net/doc/texbook.pdf) **强力推荐！！！不仅仅是TeX的使用，还有排版/设计思想**
* [The (Not So) Short Introduction to LaTeX2e](https://mirrors.ctan.org/info/lshort/english/lshort.pdf) - Very comprehensive introduction to LaTeX.
* [TEX by Topic](http://mirrors.ctan.org/info/texbytopic/TeXbyTopic.pdf) - The book describes itself as “a TEXnician’s reference”, and covers the way TEX (the engine) works in as much detail as most ordinary TEX programmers will ever need to know.
* [TeX for the Impatient](http://mirrors.ctan.org/info/impatient/cn/cnbook.pdf) -  a handbook that arose from the need to help technical writers learn TEX more quickly.

## Social media

- [Twitter: @TeXtip](https://twitter.com/TeXtip) - Tips related to (La)TeX by [John D. Cook](https://www.johndcook.com/).
- [TeX.StackExchange](https://tex.stackexchange.com) - StackExchange TeX section.


