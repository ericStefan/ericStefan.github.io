---
title: CSS基础（五）—— Position定位布局
categories: 
- web前端
description: Position定位
cover: https://s2.loli.net/2024/05/31/ACdRtH5y481DSFP.png
tags:
- css
---

# Position定位

`position`属性用于设置元素的 定位模式，由边偏移`left` `right` `top` `bottom` 属性决定最终位置。

```css
position: static | relative | absolute | fixed | sticky
```

## 1、`position: static`

指元素使用正常布局行为，使用正常文档流布局，此时`top` `bottom` `left`  `right`和层级`z-index`对其无效。 一般设置`static`用来清除定位属性。

## 2、`position: relative`

相对定位，相对原来位置进行偏移，可以使用边偏移移动， 每次移动以左上角为基点移动，原来的位置继续占有，处于标准流。

```css 
div{
    width: 100px;
    height: 100px;
}
div:first-child{
    background-color: pink;
}
div:nth-child(2){
    background-color: green;
    left: 50px;
    top: 50px;
    position: relative;
}
div:nth-child(3){
    background-color: yellow;
}
```

```html
<div>1</div>
<div>2</div>
<div>3</div>
```

<img src="C:\Users\64296\AppData\Roaming\Typora\typora-user-images\image-20211126133524034.png" alt="image-20211126133524034" style="zoom: 50%;" />

## 3、`position: absolute`

绝对定位，脱离标准流，不占用原来的位置。

```css
.father{
    width: 200px;
    height: 200px;
    background-color: yellow;
    margin: 150px;
}
.son{
    width: 100px;
    height: 100px;
    background-color: green;
}
.son:first-child{
    position: absolute;
    left: 50px;
    top: 50px;
}
```

```html
<div class="father">
     <div class="son"></div>
     <div class="son"></div>
</div>
```

 在父元素没有设置定位模式的情况下，使用绝对定位以浏览器为基点，且不占用位置。<img src="C:\Users\64296\AppData\Roaming\Typora\typora-user-images\image-20211126134345908.png" alt="image-20211126134345908" style="zoom:50%;" />

给父元素设置了`position:relative`后，则绝对定位以父亲为基准点

```css
.father{
		postion: relative;
}
```

<img src="C:\Users\64296\AppData\Roaming\Typora\typora-user-images\image-20211126134645246.png" alt="image-20211126134645246" style="zoom:50%;" />

因此在元素使用绝对定位的时候，父元素一般会设置为相对定位，“**子绝父相**”。

## 4、`position: fixed`

固定定位：

1、跟父元素定位模式无关，只认浏览器 

 2、完全脱标，不占用位置，不随滚动条滚动

## 5、`z-index`

​	1、z-index只有添加了相对、绝对、固定定位才有这个属性

​    2、z-index数字越大，在越上层,默认值为0

​    3、z-index数字相同，根据书写顺序，后来居上

## PS: 绝对定位和固定定位会把元素转换成inline -block

## 6、使用定位实现垂直水平居中

```css
.father{
            width: 400px;
            height: 400px;
            margin: 0 auto;
            background-color: pink;
            position: relative;
        }
        /* 该种垂直居中方法适用于需要绝对定位的时候 */
        .son{
            width: 100px;
            height: 100px;
            background-color: green;
            position: absolute;
            left: 50%;  /*移动父容器宽度的50%*/
            margin-left: -50px;  /*向右再移动自身宽度的一半*/
            top: 50%; /*移动父容器高度的一半*/
            margin-top: -50px; /*再向上移动自身高度的一半*/
        }
```

```html
<div class="father">
        <div class="son"></div>
</div>
```

