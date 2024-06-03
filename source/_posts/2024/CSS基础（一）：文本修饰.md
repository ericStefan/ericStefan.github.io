---
title: CSS基础（一）：文本修饰
date: 2024-06-03 11:10:02
categories: 
- web前端
description: CSS3文本修饰
cover: https://s2.loli.net/2024/05/31/iUncx7S1ahWmB6z.png
tags:
- css
---

# CSS3文本修饰

## 1、字体样式

### `color`字体颜色

使用`unicode`设置字体来提高兼容性，`\9ED1\4F53`就是"宋体",尽量只写宋体和微软雅黑的`unicode`

```css
h1 {
	color: #f00
}
```

还以使用rgb和rgba来设置颜色

```css
rgba(0, 174, 255, 0.37)
/*其中0.37为alpha的值表示透明度*/
```



### `font-size`字体大小 :

1em=1个默认字体大小(浏览器默认为16px)

### `font-family`字体类型:

1、 可以设置多个字体，当找不到前面的字体文件就会依次使用后面的字体
2、 单个单词的字体不需要加引号，存在空格#$等的字体名称必须加引号
3、需要设置英文字体时，将英文字体放在前面

```css
h1 {
	font-family: "Microsoft Yahei", "宋体", tahoma, Arial,"Hiragino Sans GB"
}
```

### `font-weight`字体粗细:

取值为100-900（整百），`lighter`,`normal`(等于400)，`bold`(等于700)，`bolder`

```css
font-weight: bold
```

### `font-style`

字体选择 `italic` 或 `oblique` 样式，默认为`normal`

### `font`

字体样式的综合写法,要按照下面的顺序来写，其中`font-size` `font-family`为必需值，前两项可以省略

```css
font: font-style font-weight font-size font-family
```

## 2、段落

### `text-align`

定义行内内容（例如文字）如何相对它的块父元素对齐。不控制块元素自己的对齐，只控制它的行内内容的对齐。

```css
text-align: left|right|center|justify
```

### `text-decoration`

用于设置文本的修饰线外观的（下划线、上划线、贯穿线/删除线 或 闪烁）,默认值为`none`，在`a`标签中默认有下划线

```css
text-decoration: underline|overline|linthrough|dotted
```

### `line-height`

设置多行元素的行高

```css
line-height: 1.5|150%|3em|20px|normal
```

在块级元素中只有一行文本，将`line-height`设置为父容器的高度值，就可实现垂直居中:

```css
div {
	width:100px;
	height:50px;
	line-heght:50px;
}
```

### `text-indent`

块元素段落首行缩进，设置为`2em`,就可实现首行两个字缩进。

### `letter-space`

字间距，对于英文就是每个字母的间距

### `word-space`

词间距，对于英文是每个单词之间的距离，对中文无效

### `text-shadow`

设置文本的阴影，其中 模糊距离`blur`为可选值

```css
text-shadow: h-shadow v-shadow blur color;
```

可以同时设置多个文本阴影：

```css
text-shadow: 1px 1px 1px #000, -1px -1px 1px #fff;  /*凸起效果*/
text-shadow: -1px -1px 1px #000, 1px 1px 1px #fff; /*凹下效果*/
```

<img src="C:\Users\64296\AppData\Roaming\Typora\typora-user-images\image-20211118220111646.png" alt="image-20211118220111646" style="zoom:33%;" />

## 3、文本显示

### `word-break`

这个属性用来设置文本内容超过盒子大小时，换行显示的方式。

```css
word-break: normal;  		/*使用默认断行*/
word-break: break-all; 	/*可以再任意字符断行，即可以拆开单词换行*/
word-break: keep-all;		/*不能拆开单词换行，连词符号是特殊情况，*/
word-break: break-word; /*与同时设置了word-break: normal 和 overflow-wrap: anywhere 具有同样的表现。*/
```

### `white-space`

常用属性值为：

```css
white-space: nowrap  /*连续空白符合并，文本换行无效， 常用来强制文本一行显示*/
```

### `text-overflow`

使用`text-overflow`属性必须设置`white-space: nowrap`和`overflow:hidden`

`text-overflow: clip`直接裁剪超出内容

``` css
white-space: norwrap;
overflow: hidden;
text-overflow: clip;
```

<img src="C:\Users\64296\AppData\Roaming\Typora\typora-user-images\image-20211126143720799.png" alt="image-20211126143720799" style="zoom:50%;" />

`text-overflow: ellipsis`超出部分用省略号代替

```css
white-space: norwrap;
overflow: hidden;
text-overflow: ellipsis;
```

<img src="C:\Users\64296\AppData\Roaming\Typora\typora-user-images\image-20211126143921835.png" alt="image-20211126143921835" style="zoom:50%;" />