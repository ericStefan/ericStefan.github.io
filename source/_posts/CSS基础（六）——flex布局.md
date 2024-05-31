---
title: CSS基础（六）—— flex布局
categories: 
- web前端
description: flex布局的原理及用法
cover: https://s2.loli.net/2024/05/31/6L8AQRcW4fIdqpP.png
tags:
- css
---

# flex布局

# 1、原理简述

采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。

![img](https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071004.png)

容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做`main start`，结束位置叫做`main end`；交叉轴的开始位置叫做`cross start`，结束位置叫做`cross end`。

项目默认沿主轴排列。单个项目占据的主轴空间叫做`main size`，占据的交叉轴空间叫做`cross size`。

使用方式：

在容器（父元素）上设置，此时子元素的`float`、`clear`和`vertical-align`属性将失效。

```css
display: flex;
```



# 2、容器(父元素)的属性

### `flex-direction`

设置主轴方向

```css
flex-direction: row | colum | row-reverse | colum-reverse
```

默认x轴为主轴，正方向为向下，y轴为父轴，正向向右

### `justify-content`

设置主轴上的布局

``` css
justify-content: flex-start | flex-end | space-around | space-between | center
```

`flex-start`  从主轴起点开始排列（默认）。

`flex-end` 从主轴结束位置开始排列（默认）。

`space-between` 最边上的两个元素分别向主轴起点和结束位置靠齐，中间元素等距排列

`space-around`  元素拥有相同的主轴方向上的两侧外边距（margin,两个相邻的元素的间距是最边上元素与容器距离的2倍）

`center`  在主轴上居中

<img src="https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071010.png" alt="img" style="zoom:50%;" />

### `flex-wrap`

设置换行方式：

```css
flex-wrap: no-wrap | wrap | wrap-reverse
```

`no-wrap` 不换行，默认值（flex布局默认在一条主轴上排列）

`wrap`    换行，第一行在上面

`wrap-reverse` 换行，第一行在下面 

### `flex-flow`

这是`flex-direction`和`flex-wrap`合写

```css
flex-flow: flex-direction  flex-wrap
```

举例：

```css
flex-flow: row wrap
```

### `align-items`

设置副轴上的布局

```css
align-items: flex-start | flex-end | center | strech | baseline
```

`flex-start`  在副轴上从轴起点开始排列

 `flex-end`  在副轴上重轴终点开始排列

`center`   在副轴上居中排列

`strech`  (默认值)如果项目未设置高度或设为auto，将占满整个容器的高度。

`baseline`: 项目的第一行文字的基线对齐。
<img src="https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071012.png" alt="img" style="zoom:50%;" />

### `align-content`

设置多根轴线的对齐方式，即有多行/多列元素，对单行/单列 不起作用

```css
align-content: flex-start | flex-end | center | space-between | space-around | stretch;
```

- `flex-start`：与交叉轴的起点对齐。
- `flex-end`：与交叉轴的终点对齐。
- `center`：与交叉轴的中点对齐。
- `space-between`：与交叉轴两端对齐，轴线之间的间隔平均分布。
- `space-around`：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
- `stretch`（默认值）：轴线占满整个交叉轴。

<img src="https://www.ruanyifeng.com/blogimg/asset/2015/bg2015071012.png" alt="img" style="zoom:50%;" />

# 3、子项（flex item）属性

### `align-self`

设置单个子项在副轴上的排列方式。可以覆盖`align-items`属性,默认值为auto.

```css
align-self: auto | flex-start | flex-end | center | baseline | stretch;
```

除auto值外，其他值的用法与`align-item`相同。

`auto`  表示继承`align-items`属性, 如果没有父元素，等同与`stretch`



### `order`

定义项目的排列顺序。数值越小，排列越靠前，默认为0, 可以为负数。

```css
order: 数字;
```

### `flex-shrink`

定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

```css
flex-shrink: <number>; 
```

```css
fle-shrink: 0; /*表示空间不足也不缩小*/
fle-shrink: 2; /*表示空间不足也2倍缩小*/
```

### `flex-grow`

`flex-grow`属性定义项目的放大比例，默认为`0`，即如果存在剩余空间，也不放大。

```css
flex-grow: <number>;
```

### `flex`

`flex`属性是`flex-grow`, `flex-shrink` 和 `flex-basis`的简写，默认值为`0 1 auto`。后两个属性可选。

```css
 flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
```

`flex`后面只填数字表示该子项占了几份。

### ` flex-basis`

`flex-basis`属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为`auto`，即项目的本来大小。

```css
 flex-basis: <length> | auto;
```

