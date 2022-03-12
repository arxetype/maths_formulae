## Preamble
* Order is difficult. Generally the following seems to work
    ```
    % !TEX TS-program = pdflatex
    % !TEX encoding = UTF-8 Unicode
    \documentclass{article}
    
    \usepackage[utf8]{inputenc}
    \usepackage[T1{fontenc}
    \usepackage[english]{babel}

    \usepackage{amsmath}
    \usepackage{amssymb}
    \usepackage{amsthm}

    % fonts

    % siunitx, bm, mathtools, other math packages

    % geometry, titlesec, titletoc and titleps/fancyhdr

    % enumitem, graphicx, booktabs, array/tabularx/longtable/multirow etc.

    % tikz and pgfplots

    % xcolor

    % hyperref
    ```
* If you copy stuff from stackoverflow, put a link to the answer. Your future self will thank you.


## Sectioning
* Use bare `\chapter`s, `\section`s etc, without any formatting such as `\large` or `\newline`. All formatting to be done in the preamble, using say package `titlesec`.
* In source code, add vertical spaces to delineate chapters and sections.
In this project, chapters are in different files, sections have two spaces and subsections have one space before them.
* Add one sentence per line. This makes it easier to see differences, and has no effect on the rendered output.


## Floats (Figures and Tables)
* In general, use `htbp` as the positioning argument. This tries the following in order
    1. `h`: Place the float *here*.
    2. `t`: Place the float at the *top* of the current page.
    3. `b`: Place the float at the *bottom* of the current page.
    4. `p`: Place the float in a special *page* for floats.

### Tables
* Follow the recommendations of package `booktabs`.
* In this project, `\toprule` and `\bottomrule` enclose the table.
* `\midrule` is used as is only once, after the header row. However, to delineate blocks, `\midrule[0.05pt]` has been used (a thinner rule than the default `\midrule`).

### Figures 
* Do not re-scale graphs made with external tools (like Python/Matplotlib or gnuplot). This will mess up the fonts. Make the figure at the size that it is to be embedded.
* While using `tikz`, externalize any complex figure that takes time to render.
    
    ```
    % Externalize Tikz Figures
    % https://tex.stackexchange.com/a/46939
    % https://tex.stackexchange.com/a/178931
    \newcommand{\externaldirectory}{tikzexternal/}
    \usetikzlibrary{external}
    \tikzexternalize[prefix=\externaldirectory]
    
    % \tikzexternaldisable
    % \tikzexternalenable
    ```


## Equations
* Don't use the `align` environment when there is only one line of equation. Use `equation` environment instead.
* There are multiple choices when one wants aligned equations. `eqnarray` is not one of them.
* Use `equation*` or `align*` for non-numbered equations. To number a select few equations one can define 
    
    ```
    \newcommand{\numberthis}{\refstepcounter{equation}\tag{\theequation}}
    ```
and invoke it for the equation to be numbered.
* Do not use `\dfrac` or `\tfrac` (or `\displaystyle`) in general. Use `\frac`. One may define

    ```
    \newcommand{\flatfrac}[2]{\ensuremath{#1/#2}}
    ```
for flattened fractions. They can then be redefined later to `\tfrac{#1}{#2}` if the author decides that flattened fractions are not in vogue.
* For differential equations use package `diffcoeff`, which handles ordinary as well as partial derivatives. One can define the differential operator separately as follows
    ```
    \newcommand{\dd}{\ensuremath{\mathop{}\! d}}
    ```
    to get the spacing before the differential operator. (`diffcoeff` also provides `\dl` whose spacing can be configured).
* Use `DeclarePairedDelimiter` from package `mathtools` for macros such as `\abs` or `\set` (for the set-builder notation). 

    ```
    \usepackage{mathtools}

    \DeclarePairedDelimiter{\abs}{\lvert}{\rvert}

    % https://tex.stackexchange.com/a/150516
    \newcommand\SetSymbol[1][]{\nonscript\:#1\vert\allowbreak\nonscript\:\mathopen{}}
    \providecommand\given{} % to make it exist
    \DeclarePairedDelimiterX\Set[1]\{\}{\renewcommand\given{\SetSymbol[\delimsize]}#1}
    ```
* Use `\DeclareMathOperator` for say `lb(x)` (log base 2) as follows
    ```
    \DeclareMathOperator{\lb}{lb}
    ```


## Fonts
In no particular order,
* mlmodern
* newpx
* newtx
* libertine + newtxmath[libertine]
* cochineal/crimson/CrimsonPro + newtxmath[cochineal]
* erewhon + newtxmath[erewhon]
* garamondx + newtxmath[garamondx]
* ETbb + newtxmath[libertine] (or maybe garamondx?)
