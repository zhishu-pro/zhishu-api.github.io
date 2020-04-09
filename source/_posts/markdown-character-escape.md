---
title: Hexo Markdown 特殊字符转义
date: 2019-04-07 00:47:28
tags: hexo markdown
---
## 特殊字符转义表
> 在使用 Markdown 编写 Hexo 的 Blog 时，对于特殊字符使用 “\” 转义有时会不成功，最好的方式是直接使用特殊字符的编码，对应如下：

```
- &#45; &minus; — 减号
! &#33; — 惊叹号Exclamation mark 
” &#34; &quot; 双引号Quotation mark 
# &#35; — 数字标志Number sign 
$ &#36; — 美元标志Dollar sign 
% &#37; — 百分号Percent sign 
& &#38; &amp; Ampersand 
‘ &#39; — 单引号Apostrophe 
( &#40; — 小括号左边部分Left parenthesis 
) &#41; — 小括号右边部分Right parenthesis 
* &#42; — 星号Asterisk 
+ &#43; — 加号Plus sign 
< &#60; &lt; 小于号Less than 
= &#61; — 等于符号Equals sign 
> &#62; &gt; 大于号Greater than 
? &#63; — 问号Question mark 
@ &#64; — Commercial at 
[ &#91; --- 中括号左边部分Left square bracket 
\ &#92; --- 反斜杠Reverse solidus (backslash) 
] &#93; — 中括号右边部分Right square bracket 
{ &#123; — 大括号左边部分Left curly brace 
| &#124; — 竖线Vertical bar 
} &#125; — 大括号右边部分Right curly brace 

```

<!-- more -->

* * *

## 编辑表格时如何输入竖线

**主要思路**： 竖线用 **&\#124;** 或者 **&\#x7C;** 来代替

**情景 1: 竖线直接用在表格里，直接用 &\#124; 代替竖线**
例如，
原始 Markdown 表格格式：
| a | r |
| - - - - - | - - - - - |
| \`a += x;\` | r1 |
| a &\#124;= y; | r2 |

显示效果：

| a | r |
| --- | --- |
| `a += x;` | r1 |
| a &#124;= y; | r2 |

* * *

**情景 2：竖线用在表格中的_代码效果_中，即用在两个反引号 \` \` 中**
这时就不要使用反引号了，直接用 **<code\> </code\>** 来代替。
例如，
原始 Markdown 表格格式：
| a | r |
| - - - - - | - - - - - |
| \`a += x;\` | r1 |
| <code\>a &\#124;= y;</code\> | r2 |

显示效果：

| a | r |
| --- | --- |
| `a += x;` | r1 |
| <code>a &#124;= y;</code> | r2 |

* * *

PS：编辑 HTML 时，输入 &amp;amp;#124; 最终可以显示为 &#124;
即用 &amp;amp; 代替 &
输入 &amp;lt;code&amp;gt; 可以显示为 <code\>