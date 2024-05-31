---
title: CSS基础（十四）—— block和inline
categories: 
- web前端
description: block和inline的区别
cover: https://s2.loli.net/2024/05/31/Ob2ZqyFuYQSkgAh.png
tags:
- css
---

## block元素：

1、单独占用一行

2、宽、高、内外边距可控制

3、默认宽度为容器的100%

4、可容纳行内元素和其他块级元素

常见的block元素：

```html
<header></header>
<nav></nav>
<address></address>
<footer></footer>
<form></form>

<div></div>
<p></p>
<h></h>
<hr/>

<ul></ul>
<ol></ol>
<li></li>
<dl></dl>

<tr></tr>
<td></td>
<table></table>

<pre></pre>
<blockquote></blockquote>
```



## inline元素：

1、和相邻元素在一行上

2、宽、高无效，可以设置水平方向的padding和margin，垂直方向无效

3、默认宽度就是内容本身宽度

4、行内元素只能容纳文本或其他行内元素（a特殊）

ps: 

1、a链接里面不能再放a

2、只有文字才能组成段落，因此块级元素p里面不能放块级元素，h1-h6,dt同理，它们都是块级元素，但不能在里面放块级元素

常见inline元素：

```html
<a></a>
<span></span>
<textarea></textarea>

<br/>
<b></b>
<del></del>
<em></em>
<i></i>
<strong></strong>
<sup></sup>
<sub></sub>
```



## inline-block元素：

存在几个特殊的行内(inline)元素标签——`<img/>` `<input/>` `<td>`，可以对它们设置宽高和对齐属性，被称为行内块级元素。

1、和相邻行内元素(行内块)在一行，但之间会有空白缝隙

2、默认宽度是内容本身

3、高度、行高、内外边距都可以控制

常见inline-block元素：

```html
<img/>、<input/>、<select></select>
```

