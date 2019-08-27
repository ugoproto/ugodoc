# Resources

- [The LATEX Project](http://www.latex-project.org/).
- [TEX](https://tex.stackexchange.com/) stack exchange.
- [Pense-bete pour natbib](http://merkel.texture.rocks/Latex/natbib.php?lang=fr).
- [CTAN](http://www.ctan.org/).
- [LaTeX Wikibook](https://en.wikibooks.org/wiki/LaTeX).
- [TeX](http://www.xm1math.net/doculatex/index.html).

# Classes

## Article

```tex
\documentclass[12pt]{article}
\title{}
\author{}
\date{}
\begin{document}
\maketitle
\begin{abstract}
...
\end{abstract}
\section{}
\subsection{}
\subsubsection{}
\paragraph{}
\subparagraph{}
\end{document}
```

## Report

```tex
\documentclass[12pt]{report}
\title{}
\author{}
\date{}
\begin{document}
\maketitle
\begin{abstract}
...
\end{abstract}
\tableofcontents
\listoffigures
\listoftables
\chapter{}
\section{}
\subsection{}
\subsubsection{}
\paragraph{}
\subparagraph{}
\end{document}
```

## Book

```tex
\documentclass[12pt]{book}
\title{}
\author{}
\date{}
\begin{document}
\maketitle
\tableofcontents
\listoffigures
\listoftables
\part{}
\chapter{}
\section{}
\subsection{}
\subsubsection{}
\paragraph{}
\subparagraph{}
\end{document}
```

# Figure

## Standard figure

```tex
%Preamble
\usepackage{graphicx}
 
%Document
\begin{figure}[htbp]
\centering
\includegraphics[width=\linewidth]{figure.png}
\caption[short for lof]{long figure caption}
\label{fig:default}
\end{figure}
\ref{fig:default}
```

## Side-by-side figure (1x2)
 
```tex
%Preamble
\usepackage[lofdepth]{subfig}
\usepackage{graphicx}

%Document
\begin{figure}[htbp] % h:here; t:top; b:bottom; p:page; default:ht
\centering
 \subfloat[short for lof][long subfigure1 caption]{
   \includegraphics[width=0.45\linewidth]{figure1.png}
   \label{subfig:fig1}
 }
 \subfloat[short for lof][long subfigure2 caption]{
   \includegraphics[width=0.45\linewidth]{figure2.png}
   \label{subfig:fig2}
}
\caption[short for lof]{long figure caption}
\label{fig:fig1}
\end{figure}
\ref{fig:fig1} and \subref{subfig:fig1}
```

## Side-by-side figure (2x2)

```tex
%Preamble
\usepackage[lofdepth,lotdepth]{subfig}
\usepackage{graphicx}
 
%Document
\begin{figure}[ht]
\centering
 \subfloat[short for lof][long subfig1 caption]{
   \includegraphics[width=0.45\linewidth]{figure1.png}
   \label{subfig:fig1}
 }
 \subfloat[short for lof][long subfig2 caption]{
   \includegraphics[width=0.45\linewidth]{figure2.png}
   \label{subfig:fig2}
}
 
 \subfloat[short for lof][long subfig3 caption]{
   \includegraphics[width=0.45\linewidth]{figure3.png}
   \label{subfig:fig3}
 }
 \subfloat[short for lof][long subfig4 caption]{
   \includegraphics[width=0.45\linewidth]{figure4.png}
   \label{subfig:fig4}
}
\caption[short for lof]{long figure caption}
\label{fig:fig1}
\end{figure}
\ref{fig:fig1} and \subref{subfig:fig1}
```

Sideways-figure

```tex
% Preamble
\usepackage{rotating}
 
% Document
\begin{sidewaysfigure}
\centering
\includegraphics{figure.png}
\caption{Sideways figure.}
\label{fig:swfig}
\end{sidewaysfigure}
```

Wrap text around figure

```tex
%Preamble
\usepackage{wrapfig, graphicx}
 
% Document
\begin{wrapfigure}{l}{0.5\textwidth} % l for left, r for right
\centering
\includegraphics[width=0.45\textwidth]{test}
\caption{Text wrapped around figure}
\label{fig:wrapfig}
\end{wrapfigure}
```

# Tables

## Standard table

```tex
\begin{table}[htbp] % h:here; t:top; b:bottom; p:page; default:ht
    \caption{default}
    \centering
    \begin{tabular}{lccr}
        \hline
        - & - & - & - \\
        \hline
        - & - & - & - \\
        - & - & - & - \\
        \hline
    \end{tabular}
    \label{tab:def}
\end{table}%
```

## Side-by-side table

```tex
%Preamble
\usepackage[lotdepth]{subfig}
 
%Document
\begin{table}[htbp] % h:here; t:top; b:bottom; p:page; default:ht
    \centering
    \subfloat[short for lot subtable1][long subtable1 caption]{
        \begin{tabular}{lccr}
            \hline
            - & - & - & - \\
            \hline
            - & - & - & - \\
            - & - & - & - \\
            \hline
        \end{tabular}
        \label{subtab:tab1}
    }
    \subfloat[short for lot subtable2][long subtable2 caption]{
        \begin{tabular}{lccr}
            \hline
            - & - & - & - \\
            \hline
            - & - & - & - \\
            - & - & - & - \\
            \hline
        \end{tabular}
        \label{subtab:tab2}
    }
    \caption[short for lot]{long table caption}
    \label{tab:tab1}
\end{table}
\ref{tab:tab1} and \subref{subtab:tab1}
```

## Sideways-table

```tex
% Preamble
\usepackage{rotating}
 
% Document
\begin{sidewaystable}
    \caption{Sideways table.}
    \centering
    \begin{tabular}{lccr}
        \hline
        - & - & - & - \\
        \hline
        - & - & - & - \\
        - & - & - & - \\
        \hline
    \end{tabular}
    \label{tab:swtab}
\end{sidewaystable}
```

## Multi-page table (longtable)

```tex
%Preamble
\usepackage{longtable}
 
% Document
\begin{center}
\begin{longtable}{|c|c|c|c|}
\caption{A simple longtable example}\\
\hline
\textbf{First entry} & \textbf{Second entry} & \textbf{Third entry} & \textbf{Fourth entry} \\
\hline
\endfirsthead
\multicolumn{4}{c}%
{\tablename\ \thetable\ -- \textit{Continued from previous page}} \\
\hline
\textbf{First entry} & \textbf{Second entry} & \textbf{Third entry} & \textbf{Fourth entry} \\
\hline
\endhead
\hline \multicolumn{4}{r}{\textit{Continued on next page}} \\
\endfoot
\hline \multicolumn{4}{r}{\textit{End of table}} \\
\endlastfoot
1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\
1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\
1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\
1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\
1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\
1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\
1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\
1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\
1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\
1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\
1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\
1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\ 1 & 2 & 3 & 4 \\
\end{longtable}
\end{center}
```

# List

## Bulleted list: itemize

```tex
\begin{itemize}
\item
\item
\item
\end{itemize}
```

## Numbered list: enumerate

```tex
\begin{enumerate}
\item
\item
\item
\end{enumerate}
```

## Description

```tex
\begin{description}
\item[]
\item[]
\item[]
\end{description}
```

## Inline enumeration

```tex
%Preamble
\usepackage{paralist}
 
%Document
\begin{inparaenum}
\item
\item
\item
\end{inparaenum}
```

# Beamer Presentation

## Table of Content

```tex
\documentclass{beamer}
\usetheme{Berkeley}
\begin{document}
 
\begin{frame}
    \tableofcontents
\end{frame}
 
\section{First}
\begin{frame}{First section slide}
    ...
\end{frame}
 
\section{Second}
%Contents with current section highlighted
\frame{\tableofcontents[currentsection]}
\begin{frame}{Second section slide}
    ...
\end{frame}
 
\end{document}
```

## List

```tex
\begin{frame}{Enumerate}
    \begin{enumerate}
        \item
        \item
        \item
    \end{enumerate}
\end{frame}
```

```tex
\begin{frame}{Itemize}
    \begin{itemize}
        \item
        \item
        \item
    \end{itemize}
\end{frame}
```

## Side-by-side figure/table/list with columns

```tex
\begin{frame}{Side-by-side figure/table/text with columns}
    \begin{columns}
        \begin{column}[C]{.45\textwidth}
% the T argument instead of C will align the top of the two columns, instead of the centers
            \rule{\textwidth}{0.75\textwidth}
        \end{column}
        \begin{column}[C]{.45\textwidth}
            \begin{enumerate} % numbered list
                \item
                \item
                \item
            \end{enumerate}
        \end{column}
    \end{columns}
\end{frame}
```

Side-by-side figure/table/list with minipage

```tex
\begin{frame}{Side-by-side figure/table/text with minipage}
    \begin{minipage}{0.45\textwidth} % figure
        \rule{\textwidth}{0.75\textwidth}
    \end{minipage}
    \qquad
    \begin{minipage}{0.45\textwidth}
        \begin{enumerate} % numbered list
            \item
            \item
            \item
        \end{enumerate}
    \end{minipage}
\end{frame}
```
