---
title: CSS基础（十三）—— 清除浮动的三种方式
categories: 
- web前端
description: css3种清除浮动的方式
cover: https://s2.loli.net/2024/05/31/FjrTPhxUvltXSim.png
tags:
- css
---

# 清除浮动的方式

## 浮动产生的问题

在父元素没有设置高度的时候，嵌套在内部的子元素使用`float`属性，会导致由于内部内容都浮在上一层，父盒子没有撑开，高度为0，这会影响后面盒子的布局。

```css
 .father{
            width: 400px;
            background-color: pink;
        }
	.son:first-child{
            width: 100px;
            height: 100px;
            background-color: green;
            float: left;
        }
	.son:nth-child(2){
            width: 100px;
            height: 100px;
            background-color: lightyellow;
            float: left;
        }
	.outer{
            width: 120px;
            height: 200px;
            background-color: red;
        }
```

```html
<div class="father">
        <div class="son"></div>
        <div class="son"></div>
</div>

    <div class="outer"></div>
```

outer类的div会根据标准流显示在son类div的下面，这不是我们想要的效果。因此需要消除浮动，**消除浮动本质是消除浮动带来的负面影响**

<img src="C:\Users\64296\AppData\Roaming\Typora\typora-user-images\image-20211123211901417.png" alt="image-20211123211901417" style="zoom:50%;" />

## 1、添加标签法

```css
clear: left|right|both
/*分别表示消除左边、右边、两边的浮动*/
```

在父元素内部浮动的盒子后面增加一`div`盒子，并设置`clear:both`就可消除浮动。

```css
.clearfix{
	clear: both;
}
```

```html
<div class="father">
        <div class="son"></div>
        <div class="son"></div>
        <div class="clearfix"></div>
    </div>
<div class="outer"></div>
```

<img src="C:\Users\64296\AppData\Roaming\Typora\typora-user-images\image-20211123212606901.png" alt="image-20211123212606901" style="zoom:33%;" />



## 2、设置overflow

给父元素设置`overflow`属性，根据BFC的特性，就可以消除浮动，但这可能会影响超出元素大小的内容显示。

```css
.father{
            width: 400px;
            background-color: pink;
  					overflow: hidden;
        }
```

## 3、添加伪元素

为了避免直接增加元素带来的结构混乱，可以使用伪元素在浮动内容后面增加一个元素来消除浮动。

```css
.clearfix::after{
    /* 使用after和before伪元素必须添加content属性，填写.占位 */
    content: "."; /*使用伪元素必须添加content，使用“.”来占位，也可填空字符*/
    display: block;  /* 将添加的元素设置为block */
    height: 0; /*设置添加元素高度为0*/
    visibility: none; /* 隐藏元素，使得content不可见 */
    clear: both;
}

.clearfix{
    /* 这是在ie6 ie7中清除浮动的方法，*是ie6 7特有的识别符 */
    *zoom:1;
}
```

```html
<div class="father clearfix">
        <div class="son"></div>
        <div class="son"></div>
    </div>
    <div class="outer"></div>
```

## 4、添加双伪元素

这种方式简化了方式3的代码

```css
.clearfix::before,
.clearfix:after
{
		content: "";
		display: table;
}
.clearfix:after{
		clear: both;
}
.clearfix{
		*zoom:1;
}

```

```html
<div class="father  clearfix">
        <div class="son"></div>
        <div class="son"></div>
    </div>

    <div class="outer"></div>
```

