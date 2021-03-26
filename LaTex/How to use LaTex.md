[TOC]
# How to use Latex

This document is a instruction about using LateX.

## 引言

@copyrights:

Author: JacksonJin

Dept: NLP Lab, Soochow University

Time: March, 2021

Content: LaTeX

Tools: Overleaf

## 1. 语法

Letax基本语法

### 1.1 导言区

主要进行一些全局内容的设置

+ \documentclass[]{}

  文档类：描述本篇文档的类型，常用的有article, book, report, letter等

  []中代表可选参数

  eg.

  [10pt]代表设置normalize字体大小，即默认字体大小，一般只有10-12pt

  [UTF8]代表使用utf-8编码

+ \title{}

  制作标题，大括号中输入标题

+ \usepackage{}

  引入一些所需要的包

+ \maketitile

  在正文区使用，使标题生效

+ \author{}

  输入作者

+ \date{}

  输入时间，可以使用\date{\today}代表今天

+ \quad

  表示空格

+ \newcommand

  定义一个新的命令

  eg.

  ```latex
  \newcommand\degree{^\circ}
  %  #定义了一个\degree命令
  %  ^表示上标,\circ表示小圆圈
  
  \newcommand\degree{^\circ}
  
  \begin{document}
      \maketitle
      直角为90\degree
      
      直角为90^\circ %效果等价
      
  \end{document}
  ```

  效果：

  ![image-20210325160336936](D:\Dev\typoraspace\notes\LaTex\imgs\fig.png)

### 1.2 正文区

+ \begin{} & \end{}

  表示文档区的开始（正文）

  ```latex
  \title{Learning Latex}
  \begin{document}
  	\maketitle
  	HelloWorld
  \end{document}
  ```

  效果图：

  ![image-20210326103312299](D:\Dev\typoraspace\notes\LaTex\imgs\fig2.png)

## 2. 数学公式

### 2.1 公式区

 $ $ 表示公式文本

  基本数学公式区同Markdown相同，与文本连续。

  eg.

  ```latex
  \begin{document}
  	\maketitle
  	Hello World
  	$f(x) = x_1 * \epsilon$
  	continue with the equation
  \end{document}
  ```

  效果图：

![image-20210326103415891](D:\Dev\typoraspace\notes\LaTex\imgs\fig3.png)

  使用双$表示新的一行书写公式：

  ```latex
  \begin{document}
  	\maketitle
  	Hello World
  	$$f(x) = x_1 * \epsilon$$
  	not continue with the equation
  \end{document}
  ```

  效果图：

  ![image-20210324152142339](D:\Dev\typoraspace\notes\LaTex\imgs\fig4.png)

### 2.2 带编号的公式

在正文区中使用**\begin{equation}  && \end{equation}**可以产生带编号的公式

eg.

```latex
\begin{document}
    \maketitle
    \begin{equation}
        f(x) = ax^2 + bx + c_1
    \end{equation}
\end{document}
```

效果图：

![image-20210326103605190](C:\Users\Jackson\AppData\Roaming\Typora\typora-user-images\image-20210326103605190.png)

## 3. 中文输入

### 3.1 如何使用中文输入

+ 1.需要在导言区导入中文包

  ```latex
  \usepackage{ctex}
  ```

+ 2.在overleaf左上角点击菜单

  ![image-20210326103629492](D:\Dev\typoraspace\notes\LaTex\imgs\fig5.png)

  编译器器选择XeLaTex，否则编译报错

  ![image-20210326103706663](D:\Dev\typoraspace\notes\LaTex\imgs\fig6.png)

+ eg.

```latex
\documentclass{article}

\usepackage{ctex}
\title{Learning Latex}

\begin{document}
    \maketitle
    Hello World
    $$f(x) = x_1 * \epsilon$$
    not continue with the equation
    中文测试：
    你好你好
\end{document}
```

+ 效果图

  ![image-20210326103807815](D:\Dev\typoraspace\notes\LaTex\imgs\fig7.png)

### 3.2 ctex宏包使用

ctex宏包同样提供了三个中文文档类document class，分别是ctexart、ctexrep和ctexbook，

分别对应latex的标准文档类article、report和book。

使用它们的时候建议将**所有涉及到的源文件**使用**UTF-8**编码

eg.

```latex
\documentclass[UTF8]{ctexart}

%\usepackage{ctex}
\title{Learning Latex}

\newcommand\degree{^\circ}

\begin{document}
    \maketitle
    Chinese Test:
    
    中文测试：
    
    你好你好
  
\end{document}
```

效果图：

![image-20210326103834753](D:\Dev\typoraspace\notes\LaTex\imgs\fig8.png)

## 4. 字体属性

在LaTex中，一个字体有5种属性：

### 4.1 **字体编码**

+ 正文字体编码：OT1、T1、EU1等

+ 数字字体编码：OML、OMS、OMX等

### 4.2 **字体族**

+ 罗马字体：笔画起笔处有装饰
+ 无衬线字体：笔画起笔处无装饰
+ 打字机字体：每个字符宽度相同，又称等宽字体

eg.

```latex
    %声明罗马字体Roman Family
    \textrm{TEXTXXXXXXXX}
    \rmfamily TEXTXXXXXXXX
    
    %声明无衬线字体Sans Serif Family
    \textsf{TEXTXXXXXXXX}
    \sffamily{TEXTXXXXXXXX}
    
    %声明打字机字体 Typewriter Family
    \texttt{TEXTXXXXXXXX}
    \ttfamily{TEXTXXXXXXXX}
```

效果图：

![image-20210326103941410](D:\Dev\typoraspace\notes\LaTex\imgs\fig9.png)

```latex
    %可以使用{}限定字体作用范围
    {\rmfamily I'm Roman Family}
    
    {\sffamily I'm Another}
    
    I am Normal
```

效果：

![image-20210326104826339](D:\Dev\typoraspace\notes\LaTex\imgs\fig10.png)

### 4.3 **字体系列**
  + 粗细
  + 宽度

eg.

```latex
%中等大小字体
\textmd{This is a Medium size}
{\mdseries This is a Medium size}

%加粗
\textbf{This is BoldFace}
{\bfseries This is BoldFace }
```

效果图：

![image-20210326105816821](D:\Dev\typoraspace\notes\LaTex\imgs\fig11.png)

### 4.4 **字体形状**
  + 直立
  + 斜体
  + 伪斜体
  + 小型大写

eg.

```
%字体形状[直立，斜体，伪斜体，小型大写]

\textup{This is 直立up}
{\upshape This is 直立up}

\textit{This is 斜体italic}
{\itshape This is 斜体italic}

\textsl{This is 伪斜体Slanted}
{\slshape This is 伪斜体Slanted}

\textsc{This is 小型大写small caps}
{\scshape This is 小型大写small caps}
```

效果图：

![image-20210326112401564](D:\Dev\typoraspace\notes\LaTex\imgs\fig12.png)

+ 中文字体设置

  需要引入ctex包

  ```latex
  \usepackage{ctex}
  
  {\songti 这是宋体} {\heiti 这是黑体} {\fangsong 这是仿宋} {\kaishu 这是楷书}
  ```

  

### 4.5 **字体大小**

```latex
%字体大小设置
{\tiny  Hello}
{\scriptsize  Hello}
{\footnotesize  Hello}
{\small  Hello}
{\normalsize  Hello}
{\large  Hello}
{\Large  Hello}
{\LARGE  Hello}
{\huge  Hello}
{\Huge Hello}
```

效果：

![image-20210326124637033](D:\Dev\typoraspace\notes\LaTex\imgs\fig13.png)

+ 如何设置中文字体大小

  需要\usepackage{ctex}

  ```latex
  %中文字号设置命令
  \zihao{5} 你好！  %5号字体中文  -5表示小五号
  ```

  效果：

  ![image-20210326125445320](D:\Dev\typoraspace\notes\LaTex\imgs\fig14.png)

## 5. LaTeX的篇章结构

### 5.1 article篇章结构

在正文区内构建不同的小节，使用\section和\subsection甚至\subsub...section命令

eg.

```latex
%导言区
\documentclass[UTF8]{article}
\usepackage{ctex}
\title{Learning Latex}
\begin{document}
    \section{摘要}
    \section{方法}
    \section{结果}
        \subsection{数据}
            \subsubsection{数据集}
    	\subsection{图标}
    	\subsection{分析}
    \section{结论}
\end{document}
```

 效果：

![image-20210326131200952](D:\Dev\typoraspace\notes\LaTex\imgs\fig15.png)

+ 在摘要中加入一段描述

```latex
\begin{document}
    \section{摘要}
    latex中文教程，包含latex中各种基本操作，论文必备！
    
    %空行表示新起一个段落，多个空行和一个空行的结果一样
    latex中文教程，15集全，包含latex中各种基本操作，论文必备！\\latex中文教程，15集全，包含latex中各种基本操作，论文必备！\par latex中文教程，15集全，包含latex中各种基本操作，论文必备！
    %\\双反斜杠表示新起一行，但并不是一个段落，会顶格开始
    %\par 产生一个新的段落，与空行命令相同
    \section{方法}
    \section{结果}
        \subsection{数据}
            \subsubsection{数据集}
    \subsection{图标}
    \subsection{分析}
    \section{结论}
\end{document}
```

效果：

![image-20210326131843721](D:\Dev\typoraspace\notes\LaTex\imgs\fig17.png)

### 5.2 ctexart的篇章结构

ctexart默认的**大标题是居中的**，如图：

![image-20210326132229145](D:\Dev\typoraspace\notes\LaTex\imgs\fig18.png)

可以通过对ctex进行设置来更改

```latex
\documentclass{ctexart}

\ctexset{
	section={
		%format用于设置章节标题全局格式，作用域为标题和编号
		%字号为小三，字体为黑体，左对齐
		%+号表示在原有格式下附加格式命令
		format+ = \zihao{-3} \heiti \raggedright,
		%name用于设置章节编号前后的词语
		%前、后词语用英文状态下,分开
		%如果没有前或后词语可以不填
		name = {,、},
		%number用于设置章节编号数字输出格式
		%输出section编号为中文
		number = \chinese{section},
		%beforeskip用于设置章节标题前的垂直间距
		%ex为当前字号下字母x的高度
		%基础高度为1.0ex，可以伸展到1.2ex，也可以收缩到0.8ex
		beforeskip = 1.0ex plus 0.2ex minus .2ex,
		%afterskip用于设置章节标题后的垂直间距
		afterskip = 1.0ex plus 0.2ex minus .2ex,
		%aftername用于控制编号和标题之间的格式
		%\hspace用于增加水平间距
		aftername = \hspace{0pt}
	},
	subsection={
		format+ = \zihao{4} \kaishu \raggedright,
		%仅输出subsection编号且为中文
		number = \chinese{subsection},
		name = {（,）},
		beforeskip = 1.0ex plus 0.2ex minus .2ex,
		afterskip = 1.0ex plus 0.2ex minus .2ex,
		aftername = \hspace{0pt}
	},
	subsubsection={
		%设置对齐方式为居中对齐
		format+ = \zihao{-4} \fangsong \centering,
		%仅输出subsubsection编号，格式为阿拉伯数字，打字机字体
		number = \ttfamily\arabic{subsubsection},
		name = {,.},
		beforeskip = 1.0ex plus 0.2ex minus .2ex,
		afterskip = 1.0ex plus 0.2ex minus .2ex,
		aftername = \hspace{0pt}
	}
}
```

效果：

![image-20210326135346776](D:\Dev\typoraspace\notes\LaTex\imgs\fig19.png)

# 6. LaTeX的特殊字符

### 6.1 空白符号

在LaTeX中，有以下注意：

+ 空行分段，多个空行等于一个
+ 自动缩进，绝对不能使用空格代替
+ 英文中多个空格处理为一个空格，中文中空格将被忽略
+ 汉字与其他字符的间距由XeLaTeX自动处理
+ 禁止使用中文全角空格

```latex
\section{空白符号}  %空格也分大小长度软硬，自行百度不同的空格
Are you     ok?   %英文中空格符号有效，但多个空格与一个空格效果相同

我很   好。这里使用了空格\quad符号哦  %中文中空格符号无效，
```

效果：

![image-20210326141920263](D:\Dev\typoraspace\notes\LaTex\imgs\fig21.png)

### 6.2 控制符

```latex
\section{控制符}
\#  \$  \%  \{  \}  \~{}  \_{}  \^{}  \&  \textbackslash %用于产生反斜杠  
```

效果：

![image-20210326143911861](D:\Dev\typoraspace\notes\LaTex\imgs\fig22.png)

### 6.3 排版符号

```latex
\section{排版符号}
\S  \P  \dag  \ddag  \copyright  \pounds
```

![image-20210326144058251](C:\Users\Jackson\AppData\Roaming\Typora\typora-user-images\image-20210326144058251.png)

### 6.4 基本符号

```latex
\section{Tex标志符号}  %这个好像没啥用
\LaTeX{}  \LaTeXe{}
```

效果：

![image-20210326152908518](D:\Dev\typoraspace\notes\LaTex\imgs\fig23.png)

### 6.5 引号

引号的表示比较奇怪

```latex
\section{引号}
%数字1左边的撇号表示左单引号，单引号字符’表示右单引号
%连续两个``表示左双引号，两个单引号表示右双引号
`HI'  ``Hello''
```

效果：

![image-20210326153356662](D:\Dev\typoraspace\notes\LaTex\imgs\fig24.png)

### 6.6 连字符

```latex
\section{连字符}
- -- ---   %连字符的个数表示连字符的长度
```

效果：

![image-20210326154913612](D:\Dev\typoraspace\notes\LaTex\imgs\fig25.png)

### 6.7 非英文字符

```latex
\section{非英文字符}  %好像也用不太上
\oe  \OE  \ae  \AE  \aa  \AA  \o  \O  \l  \L  \ss \SS  !`  ?`
```

![image-20210326155142151](D:\Dev\typoraspace\notes\LaTex\imgs\fig26.png)

### 6.8 重音符号

这个也不会用到，算了吧。。



