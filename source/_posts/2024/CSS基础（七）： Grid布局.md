---
title: CSS基础（七）：Grid布局
date: 2024-06-03 11:21:43
categories: 
- web前端
description: Grid布局
cover: https://s2.loli.net/2024/05/31/amGM5lLo3j12UHh.png
tags:
- css
- grid
---

## 一、概述

​		Flex 布局是轴线布局，只能指定"项目"针对轴线的位置，可以看作是**一维布局**。Grid 布局则是将容器划分成"行"和"列"，产生单元格，然后指定"项目所在"的单元格，可以看作是**二维布局**。Grid 布局远比 Flex 布局强大。

## 二、基本概念

### 2.1 容器和项目

最外层的元素`<div>`就是容器（container）,内层的元素`<div>`就是项目（item）

```html
<div>
  <div><p>1</p></div>
  <div><p>2</p></div>
  <div><p>3</p></div>
</div>
```

### 2.2 行和列

​		容器里面的水平区域称为行（row）,垂直区域称为列（column）。

![](https://s2.loli.net/2024/04/19/7uKFBg9jUOSleZp.png)

### 2.3 单元格

​		行和列的交叉区域，称为单元格（cell）。n行和m列会生成n x m个单元格。

### 2.4 网格线

​		划分网格的线，称为"网格线"（grid line）。水平网格线划分出行，垂直网格线划分出列。正常情况下，`n`行有`n + 1`根水平网格线，`m`列有`m + 1`根垂直网格线。

![](https://s2.loli.net/2024/04/19/VyN3pGUZEMiPnjY.png)

## 三、容器属性

### 3.1 display

​		**`display:grid`** : 指定一个容器为网格布局。

​		**`display:inline-grid`** : 将容器元素设为行内元素。(设置为grid布局后默认为`block`布局)

```css
div{
	display:grid;
	display:inline-grid;
}
```

​		**PS：**设为网格布局以后，容器子元素（项目）的`float`、`display: inline-block`、`display: table-cell`、`vertical-align`和`column-*`等设置都将失效。

### 3.2 grid-template-columns 和grid-template-rows

​		**`grid-template-columns`**：属性定义每一列的列宽。

​		**`grid-template-rows`**：属性定义每一行的行高。

指定一个三行三列的网格，列宽行宽都是100px：

```css
.container{
	display:grid;
	grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
}
```

使用百分比：

```css
.container{
	display:grid;
	grid-template-columns: 33.33% 33.33% 33.33%;
  grid-template-rows: 33.33% 33.33% 33.33%;
}
```

#### （1）`repeat()`

使用`repeat()`函数可以简化添加重复的值：

```css
//第一个参数表示重复的数量，第二和阐述表示值
grid-template-columns:repeat(3,33.33%);
//也可以重复特定的模式
grid-template-columns: repeat(2, 100px 20px 80px);
```

#### （2）`auto-fill`关键字

容器大小不确定，单元格大小固定，为了使每一行（或每一列）容纳尽可能多的单元格，使用`auto-fill`自动填充

```css
.container {
  display: grid;
  grid-template-columns: repeat(auto-fill, 100px);
}
```

#### （3）`auto-fit`关键字

用法与`auto-fill`基本一致，当容器足够宽，可以在一行容纳所有单元格，并且单元格宽度不固定的时候，才会有欣慰差异：`auto-fill`会用空格子填满剩余宽度，`auto-fit`则会尽量扩大单元格的宽度。

#### （4）fr关键字

`fr`关键字（fraction 的缩写，意为"片段"）：如果两列的宽度分别为`1fr`和`2fr`，就表示后者是前者的两倍。

```css
.container {
  display: grid;
  //两个相同宽度的列
  grid-template-columns: 1fr 1fr;
}
```

`fr`与绝对长度结合使用

```css
.container {
  display: grid;
  grid-template-columns: 150px 1fr 1fr;
}
```

#### （5）`minmax()`

`minmax()`函数产生一个长度范围，表示长度就在这个范围之中。它接受两个参数，分别为最小值和最大值。

```css
grid-template-columns: 1fr 1fr minmax(100px, 1fr);
```

#### （6）`auto`关键字

`auto`关键字表示由浏览器自己决定长度。

```css
grid-template-columns: 100px auto 100px;
```

#### （7）网格线名称

`grid-template-columns`属性和`grid-template-rows`属性里面，还可以使用方括号，指定每一根网格线的名字，方便以后的引用。

```css
.container{
  display: grid;
  grid-template-columns: [c1] 100px [c2] 100px [c3] auto [c4];
  //一根线允许有多个名称
  grid-template-rows: [r1] 100px [r2] 100px [r3 row-3] auto [r4];
}
```

### 3.3 `row-gap` , `column-gap` , `gap` 

`row-gap`：设置行与行的间隔。

`column-gap`：设置列与列的间隔。

```css
.container {
  row-gap: 20px;
  column-gap: 20px;
}
```

`gap`：是`row-gap`和`column-gap`的合并写法。

```css
//第二个值省略的话，浏览器默认第二个值等于第一个值
gap: <row-gap> <column-gap>;
```

**PS**：在旧标准中这三个属性名前面有'grid-'前缀，在新标准中删除

### 3.4 `grid-template-areas`

`grid-template-areas`：属性用于定义区域。

```css
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
  //a-i 9个字母分别对应9个单元格
  grid-template-areas: 'a b c'
                       'd e f'
                       'g h i';
}
```

### 3.5 grid-auto-flow 

`gird-auto-flow`：决定容器内子元素的方式方式，默认值为`row`（先行后列），也可以设置为`column`(先列后行)。

```css
grid-auto-flow: column;
```

后面添加`dense`，表示尽可能紧密填满，尽量不出现空格。

```css
grid-auto-flow: row dense;
grid-auto-flow: column dense;
```

### 3.6 justify-items， align-items， place-items

`justify-items`：设置单元格内容的水平位置（左中右）。

`align-items`：设置单元格内容的垂直位置（上中下）。

`place-items`：是`align-items`属性和`justify-items`属性的合并简写形式。

```css
.container {
  justify-items: start | end | center | stretch;
  align-items: start | end | center | stretch;
}
```

```css
//第二个值被省略，则默认第二个值与第一个值相同
place-items: <align-items> <justify-items>;
```

对应值的含义：

```
start：对齐单元格的起始边缘。
end：对齐单元格的结束边缘。
center：单元格内部居中。
stretch：拉伸，占满单元格的整个宽度（默认值）。
```

### 3.7 justify-content， align-content， place-content

`justify-content`：整个内容区域在容器里面的水平位置（左中右）。

` align-content `：整个内容区域的垂直位置（上中下）。

`place-content`：`place-content`属性是`align-content`属性和`justify-content`属性的合并简写形式。

```css
.container {
  justify-content: start | end | center | stretch | space-around | space-between | space-evenly;
  align-content: start | end | center | stretch | space-around | space-between | space-evenly;  
}
```

对应属性值的含义：

```
start：对齐容器的起始边框。
end：对齐容器的结束边框。
center：容器内部居中。
stretch：项目大小没有指定时，拉伸占据整个网格容器。
```

```
space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与容器边框的间隔大一倍。
```

![](https://s2.loli.net/2024/04/19/a5RY6CrcS8zDklT.png)

```
space-between：项目与项目的间隔相等，项目与容器边框之间没有间隔。
```

![](https://s2.loli.net/2024/04/19/NbQVMHy1U3k8xLf.png)

```
space-evenly：项目与项目的间隔相等，项目与容器边框之间也是同样长度的间隔。
```

![](https://s2.loli.net/2024/04/19/RW5MtgY9x4Q2n6O.png)

### 3.8 grid-auto-columns， grid-auto-rows

`grid-auto-columns`属性和`grid-auto-rows`属性用来设置，浏览器自动创建的多余网格的列宽和行高。它们的写法与`grid-template-columns`和`grid-template-rows`完全相同。

如果不指定这两个属性，浏览器完全根据单元格内容的大小，决定新增网格的列宽和行高。

下面的例子里，划分好的网格是3行 x 3列，但是，8号项目指定在第4行，9号项目指定在第5行。

```css
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
  grid-auto-rows: 50px; 
}
```

![](https://s2.loli.net/2024/04/19/Gej21z6BJmYDpNc.png)

### 3.9 grid-template， grid

`grid-template`：`grid-template-columns`、`grid-template-rows`和`grid-template-areas`这三个属性的合并简写形式。

`grid`：`grid-template-rows`、`grid-template-columns`、`grid-template-areas`、 `grid-auto-rows`、`grid-auto-columns`、`grid-auto-flow`这六个属性的合并简写形式。

## 四、项目属性

### 4.1 grid-column-start， grid-column-end， grid-row-start， grid-row-end

这四个属性用来定位项目的四个边框，分辨定位在哪根网格线

`grid-column-start`：左边框所在的垂直网格线
`grid-column-end`：右边框所在的垂直网格线
`grid-row-start`：上边框所在的水平网格线
`grid-row-end`：下边框所在的水平网格线

使用数字表示第几根网格线：

```css
.item-1 {
  grid-column-start: 1;
  grid-column-end: 3;
  grid-row-start: 2;
  grid-row-end: 4;
}
```

使用网格线名字：

```css
.item-1 {
  grid-column-start: header-start;
  grid-column-end: header-end;
}
```

这4个属性值可以使用`span`,表示 “跨越”，即左右边框（上下边框）之间跨越多少个网格。

```css
.item-1 {
  //表示图中的1
  grid-column-start: span 2;
}
```

![](https://s2.loli.net/2024/04/19/r75oSWIFgBbyZje.png)

### 4.2 grid-column， grid-row

`gird-column`：`grid-column-start`和`grid-column-end`的合并简写形式。

`grid-row`：`grid-row-start`属性和`grid-row-end`的合并简写形式。

```css
.item {
  grid-column: <start-line> / <end-line>;
  grid-row: <start-line> / <end-line>;
}
```

```css
.item-1 {
  grid-column: 1 / 3;
  grid-row: 1 / 2;
}
```

这两个属性之中，也可以使用`span`关键字，表示跨越多少个网格。

```css
.item-1 {
  background: #b03532;
  grid-column: 1 / span 2;
  grid-row: 1 / span 2;
}
```

### 4.3 grid-area

`grid-area`：指定项目放在哪一个区域。

```css
#container{
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
  grid-template-areas: 'a b c'
                     'd e f'
                     'g h i';
}
.item-1 {
  //1在图中的e位置
  grid-area: e;
}
```

![](https://s2.loli.net/2024/04/19/ujHWeDsP1IFSJpE.png)

### 4.4 justify-self， align-self， place-self

`justify-self`：设置单元格内容的水平位置（左中右），跟`justify-items`属性的用法完全一致，但只作用于单个项目。

`align-self`：设置单元格内容的垂直位置（上中下），跟`align-items`属性的用法完全一致，也是只作用于单个项目。

```css
.item {
  justify-self: start | end | center | stretch;
  align-self: start | end | center | stretch;
}
```

```
start：对齐单元格的起始边缘。
end：对齐单元格的结束边缘。
center：单元格内部居中。
stretch：拉伸，占满单元格的整个宽度（默认值）。
```

`place-self`：`align-self`属性和`justify-self`属性的合并简写形式。

```css
place-self: <align-self> <justify-self>;
```

