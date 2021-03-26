[TOC]
# How to use Latex

This document is a instruction about using Latex.

Author: JacksonJin

Tools: Overleaf

## 1.语法

Letax基本语法

### 1.1导言区

主要进行一些全局内容的设置

+ \documentclass[]{}

  文档类：描述本篇文档的类型，常用的有article, book, report, letter等

  []中代表可选参数

  eg.

  [10pt]代表设置normalize字体大小，即默认字体大小，一般只有10-12pt

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

## 2.数学公式

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

## 3.中文输入

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

## 4.字体属性

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