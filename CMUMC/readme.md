# 全国大学生数学建模竞赛LaTeX模板使用说明

**注** 该模板基于[LaTeX工作室的CMUMCThesis模板](https://github.com/latexstudio/CUMCMThesis.git), 该模板只适用于个人学习使用, 切勿用于商业用途.

# 基本模板及说明

```latex{.line-numbers}

\documentclass[]{cumcmthesis}

    %指定使用该模板, 需将cumcmthesis.cls文件于tex文件置于同一目录下
    % 可选参数,加在[]中
    % - withoutpreface:提交电子版时,无需承诺书和封面
    % - bwprint:黑白打印,默认为colorprint

\title{论文题目}
\tihao{A}            % 题号
\baominghao{4321}    % 报名号
\schoolname{你的大学}
\membera{成员A}
\memberb{成员B}
\memberc{成员C}
\supervisor{指导老师}
\yearinput{2017}     % 年
\monthinput{08}      % 月
\dayinput{22}        % 日

\begin{document}

\maketitle % 承诺书与封面页

    

% 摘要
\begin{abstract}

    摘要的具体内容。
    \keywords{关键词1\quad  关键词2\quad   关键词3}

\end{abstract}

\tableofcontents %目录, 不需要目录时, 注释掉即可

\section{问题重述}

    \subsection{问题背景}

    \subsection{目标任务}

\subsection{问题分析}

\section{模型假设}

\section{符号说明}

    \begin{center}
        \begin{tabular}{cc}
            \hline
            \makebox[0.3\textwidth][c]{符号}	&  \makebox[0.4\textwidth][c]{意义} \\ 
            \hline
            D	    & 木条宽度（cm） \\ 
            \hline
        \end{tabular}
    \end{center}

\section{模型的建立与求解}

\section{灵敏度分析}

\section{模型的评价与推广}

% 参考文献
\begin{thebibliography}{99}%宽度99

    \bibitem{bib:one} ....

\end{thebibliography}

% 附录
\begin{appendices}

    附录的内容。

\end{appendices}

\end{document}

```

文章的内容结构大致为:问题重述(包含问题背景和任务目标),问题分析,模型假设,符号说明,
模型的建立与求解(问题一,问题二,$\cdots$),灵敏度分析,模型的评价与推广,参考文献,附录

文章需用xelatex编译

```shell
xelatex example
or
latexmk -xelatex example
```

# 语法

## 引用说明

由 `heperref` 和 `cleveref` 宏包里的 `\cref` 来代替原来的 `\ref` :

* 原先引用时, 例如引用图片, 需要使用`引用图\ref{xxx}`
* 现在引用时, 不需要说明是图, 还是表$\cdots$, 只需在引用时用`\cref`代替即可, 同时, 引用后还具有超链接功能

## 位置参数

图片和表格需要指定其在文中的位置, 可以用以下参数:

* h: here
* b:bottom
* t:top
* p:page

默认使用hbtp(不分顺序), !h将强制在这里.

## 图片

同时需注意, 位图尽量用jpg, png格式; 矢量图用png格式. 图片若未指定后缀, 则按**.pdf, .eps, .jpg, .png**的顺序搜索.
图片的默认搜索文件夹为 `\graphicspath{{figures/}{figure/}{pictures/}%{picture/}{pic/}{pics/}{image/}{images/}}` , 
因此, 只需将图片放在与tex文件相同根目录的其中一个文件夹下即可.

以下是插入图片的语法:

```latex{.line-numbers}

% 单张图片
\begin{figure}[! H]

	\centering
	\includegraphics[width=0.6\textwidth]{file name}
	\caption{picture name}
	\label{my label}

\end{figure}

% 插入单张过宽图片
\begin{figure}[H]

	\centering
	\includegraphics[width=0.6\textwidth][center]{file name}
	\caption{picture name}
	\label{my label}%%后文用\ref{my label}引用

\end{figure}

% 插入两张图片并并排
\begin{figure}[! H]

	\centering
	\begin{minipage}[c]{0.48\textwidth}
		\centering
		\includegraphics[width=0.8\textwidth]{file name}
		\subcaption{picture name}
        \label{}
	\end{minipage}
	\begin{minipage}[c]{0.48\textwidth}
		\centering
		\includegraphics[width=0.8\textwidth]{file name}
		\subcaption{picture name}
        \label{}
	\end{minipage}
    \caption{}
    \label{}

\end{figure}

% 插入三张图片并排显示
\begin{figure}[! H]

	\centering
	\begin{minipage}[c]{0.3\textwidth}
		\centering
		\includegraphics[width=0.95\textwidth]{file name}
		\subcaption{picture name}
        \label{}
	\end{minipage}
	\begin{minipage}[c]{0.3\textwidth}
		\centering
		\includegraphics[width=0.95\textwidth]{file name}
		\subcaption{picture name}
        \label{}
	\end{minipage}
	\begin{minipage}[c]{0.3\textwidth}
		\centering
		\includegraphics[width=0.95\textwidth]{file name}
		\subcaption{picture name}
        \label{}
	\end{minipage}
    \caption{}
    \label{}

\end{figure}

% 并排插入两个不同高的图片
\begin{figure}[! H]

    \centering
    \begin{minipage}[c]{0.48\textwidth}
        \centering
        \includegraphics[height=0.2\textheight]{file name}
        \subcaption{}
    \end{minipage}
    \begin{minipage}[c]{0.48\textwidth}
        \centering
        \includegraphics[height=0.2\textheight]{file name}
        \subcaption{}
    \end{minipage}
    \caption{多图并排示例}

\end{figure}

```

## 表格

一般表格,用该[网站](https://www.tablesgenerator.com/latex_tables)生成

三线表:
```latex{.line-numbers}
\begin{table}[!htbp]
    \caption{中文标题}
    \label{}
    \centering
    \begin{tabular}{cc...c}
        \toprule[1.5pt]
        表头第1个格   & 表头第2个格   & ... & 表头第n个格  \\
        \midrule[1pt]
        表中数据(1,1) & 表中数据(1,2) & ... & 表中数据(1,n)\\
        表中数据(2,1) & 表中数据(2,2) & ... & 表中数据(2,n)\\
        ...................................................\\
        表中数据(m,1) & 表中数据(m,2) & ... & 表中数据(m,n)\\
        \bottomrule[1.5pt]
    \end{tabular}
\end{table}
```

**tabular**右边的字符个数表示列数, c为居中, l为左对齐, r为右对齐. 在字符间添加**@{文本}**, 其文本会被插入每一行对应位置
在字符间加 `|` 可以添加分隔线

表格以 `\\` 分行, \hline表示分隔线.**{booktabs}宏包**提供了 `\toprule,\midrule,\bottomrule` 来绘制三线表, 可选参数可以指定线宽

## 公式

### 行内公式

用 `$$` 包裹

### 行间公式

#### 单行公式

不需要编号时, 可以用 `\[ \]` 包裹

需要编号时, 可以用**equation**(只支持单行)环境, 并加上 `\label{}`

```latex
\begin{equation}
xxx
\label{}
\end{equation}
```

同时, 注意用 `\cref` 引用

#### 多行公式

可以用**align**数学环境:

```latex
\begin{align}
P & = UI \\
  & = I^2R
\end{align}
```

符号 `&` 用来对齐特定位置, 每行可以有多个, 但每行的个数需要相同. 符号 `\\` 用来换行, 可在不需要编号的行加上 `\notag` , 这样其就不会有编号

### 输入矩阵

```latex
\[
\mathbf{X} = \left(
    \begin{array}{cccc}
    x_{11} & x_{12} & \ldots & x_{1n}\\
    x_{21} & x_{22} & \ldots & x_{2n}\\
    \vdots & \vdots & \ddots & \vdots\\
    x_{n1} & x_{n2} & \ldots & x_{nn}\\
    \end{array} \right)
\]
```

即左右的括号用 `\left,\right` 来匹配内容大小, 中间用**array**环境来输入内容.

### 分段函数

```latex
\[
f(x) =
    \begin{cases}
        0 &  x \text{为无理数} ,\\
        1 &  x \text{为有理数} .
    \end{cases}
\]
```

置于**case**环境之中, 用 `\\` 换行

### 字体

公式环境中, 字体是数学字体, 与正文字体不同, 若公式中有个别文字, 则需放在 `\text{}` 之中

需要加粗的字母用 `\bm{}` 包裹上.

## 自定义环境

注: 以下内容都可用 `\cref` 引用

用法示例

```latex
\begin{definition}
    定义环境
    \label{}
\end{definition}
```

该语句可以使用定理环境, 可以在后文方便地用 `cref{label}` 的方法来引用该定义

该文档类中, 包含的自定义环境有:
* 定义 definition
* 定理 theorem
* 引理 lemma
* 推论 corollary
* 假设 assumption
* 猜想 conjecture
* 公理 axiom
* 定律 principle
* 问题 problem
* 例子 example
* 证明 proof
* 解 solution

## 脚注
`\footnote{内容}`可以生成脚注

## 列表

### 有序列表
```latex
\begin{enumerate}
    \item one
    \item two
    \item ...
\end{enumerate}
```

### 无序列表
```latex
\begin{itemize}
    \item one
    \item two
    \item ...
\end{itemize}
```

### 更改列表编号

经过查阅资料,常规的修改列表编号的方法都是引入**enumerate**的宏包,然后再列表环境中添加可选参数`A,(1),step 1`之类的来修改
列表编号.但一开始,我在文件中引入该宏包后,发现会报错.经过比较,才发现该宏包与**enumitem**宏包会产生冲突.[具体见此](https://tex.stackexchange.com/questions/519981/whats-the-difference-between-the-enumerate-and-enumitem-packages)

<!-- **enumitem**宏包修改列表编号样式的方法:添加可选参数`label=<commands>` -->

在引入**enumitem**宏包时,添加可选参数`[shortlabels]`,后面修改列表编号时,可以像**enumerate**宏包一样简便地修改:
```latex
\begin{enumerate}

## 字体加粗与斜体
用`\textbf{}`对文本进行加粗,`\textbf{}`对文本进行斜体

注:中文并不支持斜体,同时,有些字体也不支持粗体,如宋体.该模板用**xeCJK**设置文章的字体为主要宋体,同时,粗体为黑体,斜体为楷书.

## 文献引用
```latex
\begin{thebibliography}{99}
    \bibitem[1] ...
\end{thebibliography}
```
在文中用`\cite{1}`即可引用,若要使参考文献标号在右上角,则用`\upcite`或`\supercite`[^1]引用

[^1]:使用`\supercite`的标号更小

引用格式:
- 书籍 [编号] 作者，书名，出版地：出版社，起止页码，出版年。
- 期刊 [编号] 作者，论文名，杂志名，卷期号：起止页码，出版年。
- 网上资源 [编号] 作者，资源标题，网址，访问时间（年月日）。

