

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

