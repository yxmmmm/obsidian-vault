

### 1. 希腊字母 (Greek Letters)

| **符号**     | **命令**     | **符号**   | **命令**   |
| ---------- | ---------- | -------- | -------- |
| $\alpha$   | `\alpha`   | $\beta$  | `\beta`  |
| $\gamma$   | `\gamma`   | $\delta$ | `\delta` |
| $\epsilon$ | `\epsilon` | $\zeta$  | `\zeta`  |
| $\eta$     | `\eta`     | $\theta$ | `\theta` |
| $\lambda$  | `\lambda`  | $\mu$    | `\mu`    |
| $\pi$      | `\pi`      | $\sigma$ | `\sigma` |
| $\phi$     | `\phi`     | $\omega$ | `\omega` |
| $\Delta$   | `\Delta`   | $\Omega$ | `\Omega` |

---
### 2. 关系运算符 (Relations)

| **符号**    | **命令**         | **符号**      | **命令**         |
| --------- | -------------- | ----------- | -------------- |
| $\le$     | `\le` 或 `\leq` | $\ge$       | `\ge` 或 `\geq` |
| $\neq$    | `\neq`         | $\approx$   | `\approx`      |
| $\sim$    | `\sim`         | $\propto$   | `\propto`      |
| $\ll$     | `\ll`          | $\gg$       | `\gg`          |
| $\in$     | `\in`          | $\notin$    | `\notin`       |
| $\subset$ | `\subset`      | $\subseteq$ | `\subseteq`    |

---

### 3. 算术与微积分 (Operators & Calculus)

| **符号** | **命令**      | **示例代码**                                                                      |
| ------ | ----------- | ----------------------------------------------------------------------------- |
| 乘号     | `\times`    | $a \times b$                                                                  |
| 除号     | `\div`      | $a \div b$                                                                    |
| 分数     | `\frac{}{}` | `\frac{a}{b}` $\rightarrow$ $\frac{a}{b}$                                     |
| 根号     | `\sqrt{}`   | `\sqrt[n]{x}` $\rightarrow$ $\sqrt[n]{x}$                                     |
| 累加     | `\sum`      | `\sum_{i=1}^{n}` $\rightarrow$ $\sum_{i=1}^{n}$                               |
| 积分     | `\int`      | `\int_{a}^{b}` $\rightarrow$ $\int_{a}^{b}$                                   |
| 偏导     | `\partial`  | `\frac{\partial y}{\partial x}` $\rightarrow$ $\frac{\partial y}{\partial x}$ |
| 极限     | `\lim`      | `\lim_{x \to 0}` $\rightarrow$ $\lim_{x \to 0}$                               |

---

### 4. 逻辑与集合 (Logic & Sets)

| **符号**     | **命令**     | **符号**       | **命令**       |
| ---------- | ---------- | ------------ | ------------ |
| $\forall$  | `\forall`  | $\exists$    | `\exists`    |
| $\infty$   | `\infty`   | $\emptyset$  | `\emptyset`  |
| $\nabla$   | `\nabla`   | $\therefore$ | `\therefore` |
| $\because$ | `\because` | $\implies$   | `\implies`   |
| $\cap$     | `\cap`     | $\cup$       | `\cup`       |

---

### 5. 箭头与修饰符 (Arrows & Accents)

|**符号**|**命令**|**符号**|**命令**|
|---|---|---|---|
|$\to$|`\to`|$\leftarrow$|`\leftarrow`|
|$\leftrightarrow$|`\leftrightarrow`|$\uparrow$|`\uparrow`|
|$\hat{a}$|`\hat{a}`|$\bar{a}$|`\bar{a}`|
|$\tilde{a}$|`\tilde{a}`|$\vec{a}$|`\vec{a}`|
|$\dots$|`\dots`|$\vdots$|`\vdots`|

# 语法



## include



```latex
\documentclass{article}
\usepakage{}
\begin{document}

i love singing
\include{chapter1}
\include{chapter2}

\end{document}
```

​													main.tex

```latex
\section{cha1}
i love dancing
```

​													chapter1.tex

```latex
\section{cha2}
i love rapping
```



但是include命令会把内容另起一页，因此使用范围不够广



## input

纯粹的文章内容插入

```
\input{filename}
```



## includeonly

用于导言区域，正文不在列表范围的include不会生效

```
\includeonly{<filename1>,<filename2>}
```



## 换行

```
\par
```

或直接换行，但是换多行只会渲染出换一行

## 原格式打印

```
\verb|"taget"|
```

## 注释

```
%这是一段注释
```

## 转义字符

反斜杠转译

```
\textbackslash
```

## 断行

段中断行，并非新段

```
\newline
or 
\\
```

## 断页

```
\newpage %双栏排版时跳到第二栏上
\clearpage %跳到新页
```



# 文章元素

## 标题

### 一级标题

带编号

```
\section{}
```

不带编号

```
\section*{}
```



### 二级标题

```
\subsection{}
```

不带编号

```
\subsection*{}
```

### 三级标题

```
\subsubsection{}
```



## 部分

```
\part
```

首字母自动大写



## 目录

```
\tableofcontents
```



## 附录

```
\appedix
```



## 标题页

```
\title{}
\author{}
\date{}

\begin{document}

\maketitle

\end{document}
```



## 引用

```
\label{be_labeled}

\ref{be_labeled}%引用章节号
\pageref{be_labeled}%页号
```

## 脚注

```
\footnote{}
```

## 分层

123顺序编号，enumerate

```
\begin{enumerate}
 \item  
  \begin{enumerate}
    \item[*]
  \end{enumerate}
  
 \item
\end{enumerate}
```

。编号，itemize

```
\begin{itemize}
	\item  
\end{itemize}
```

Description,加粗目标

```
\begin{Description}
	\item[加粗部分]。。。
\end{Description}
```



# 对齐环境

## 居中

```
\begin{center}

\end{center} %块级

\centering%后续
```

## 左右对齐

```
\raggedright
\raggedleft
```



# 引用环境

```
\begin{quote}

\end{quote}%较短


\begin{quotation}

\end{quotation}%段落
```



# 摘要环境

```
\begin{abstract}

\end{abstract}
```



# 代码环境

```
\begin{verbatim}

\end{verbatim}
```



# 表格环境

上模版

# 插图

放入同一个目录下可直接用图片名字

```
\usepackage{graphicx}

%假设主图在figure文件夹，标志在logo文件夹，但是会先在根目录中寻找，所以要注意同名问题
graphicspath{{figures/}{logos/}}
%想居中可加begin{center}
\includegraphics[scale/height/width/angle=< >]{}

```



# 浮动体

```latex
\listoffigures%图片目录
\listoftables%表格目录

\caption%带编号
\caption*%不带编号

\begin{table/figure}

\end{table/figure}
```



# 盒子

```
\parbox[<align>][<height>][<inner-align>]{<width>}{...}%段级


\begin{minipage}[<align>][<height>][<inner-align>]{<width>}
...

\end{minipage}
```

![image-20260123105856659](/Users/yangxiaomao/Library/Application Support/typora-user-images/image-20260123105856659.png)

### 并排（共用标题）

```
\begin{figure}[htbp]%全打开

\centering
\includegraphics[width=...]{}
\qquad%并排图片间空格
\includegraphics[width=...]{}\\[...pt]
\includegraphics[width=...]{}
\caption{}

\end{figure}
```

### 子图（各有标题）

```
\begin{figure}[htbp]%全打开

	\centering
	\begin{subfigure}{<width>}%使用subcaption宏包的subfigure环境排版子图.width必填例如5cm / 0.45\textwidth
		\centering
		\icludegraphics[width=...]{...}
		\caption{...}
	\end{subfigure}
	
	\qquad
	
	begin{subfigure}{...}
		\centering
		\icludegraphics[width=...]{...}
		\caption{...}
	\end{subfigure}

\end{figure}
```



# 数学公式排版

### 行内公式

一对$

```
The Pythagorean theorem is
$a^2+b^2=c^2$
```

渲染结果

The Pythagorean theorem is $a^2+b^2=c^2$

### 行间公式

```
The Pythagorean theorem is:
\begin{equation}
a^2 + b^2=c^2 \label{pythagorean}
\end{equation}
Equation \eqref{pythagorean} iscalled`Gougu theorem' in Chinese
```

![image-20260123142418442](/Users/yangxiaomao/Library/Application Support/typora-user-images/image-20260123142418442.png)

可用\tag修改公式编号

\notag/ \nonumber/ \begin{equaton*}取消公式编号

# 字体&字号

![image-20260124195554779](/Users/yangxiaomao/Library/Application Support/typora-user-images/image-20260124195554779.png)



# 段落格式&间距

## 行距

```
\linespread{<factor>}
```



## 段落格式

```
\setlength{\leftskip}{(length)}
\setlengthf\rightskip}{(length)}
\setlength{\parindent}{(length)}
```



## 水平间距

![image-20260124200608938](/Users/yangxiaomao/Library/Application Support/typora-user-images/image-20260124200608938.png)

## 垂直间距

![image-20260124200718144](/Users/yangxiaomao/Library/Application Support/typora-user-images/image-20260124200718144.png)



# 参考文献

1. 复制bibtex信息到--.bib文件
2. 导言区\bibliographystyle{plain}
3. 正文引用处\cite{key}
4. 结尾/bibliography{bib文件名}
5. xetex运行一次，bibtex运行一次，xetex运行两次



