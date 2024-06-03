---
title: CSS基础（二）：盒子模型
date: 2024-06-03 11:12:08
categories: 
- web前端
description: CSS盒模型
cover: https://s2.loli.net/2024/05/31/S7Up6oMwmzubE8i.png
tags:
- css
---

# CSS盒模型

## 1、border(边框)

`border-width` 边框宽度

`border-style`: 边框样式

```
none:无边框（默认）

solid:单实线

dashed:虚线

dotted:点线

double:双实线
```

`border-color` 边框颜色

```css
/*综合写法*/
border: border-width || border-style || border-color
```

可以分别对上下左右四个边框进行修饰：

```css
border-top-width: 10px;
border-top-style: solid;
border-top-color: #3e3e3e;
/*
border-top: 10px solid #3e3e3e;
*/
```

`border-collapse`

```css
border-collapse: collapse;/*合并边框*/

border-collapse: separate;/*边框分离*/
```

`border-radius` 边框的曲率

```css
border-radius: 10px 10px 10px 10px /*左上 右上 右下 左下*/

border-radius: 10% 20% 30% /*左上 右上和左下 右下*/

border-radius: 25% 25% /*左上和右下 右上和左下*/

border-radius:50% /*四个角*/
```

## 2、padding(内边距)

```css
padding: 上边距 右边距 下边距 左边距;
```

```css
padding-top: 10px;
```

在IE6中行内元素没有padding, 在chrome中显示也存在问题，一般只给行内元素设置左右padding。

盒子没有设置高度/宽度，或者继承了高度/宽度，padding不会影响盒子宽度/高度。

## 3、margin(外边距)

将一个具有宽度的block元素左右margin设置为`auto`就可实现水平居中

```css
div{
	width:100px;
	height: 100px;
	background-color: black;
	margin: 0 auto;
}
```

行内元素只有左右外边距，没有上下外边距。

## 4、margin重叠（塌陷）

在垂直方向上的两个盒子的margin会出现重叠现象：

```css
div{
            width: 100px;
            height: 100px;
            background-color: yellow;
        }

        div:first-child{
            margin-bottom: 20px;
        }
        div:nth-child(2){
            background-color: purple;
            margin-top: 10px;
        }
```

```html
   <div></div>
    <div></div>
```

两个div的上下maigin为20px:

<img src="C:\Users\64296\AppData\Roaming\Typora\typora-user-images\image-20211122001948158.png" alt="image-20211122001948158" style="zoom:67%;" />

此时它们的上下margin取两个之间的较大的值。

解决方案：避免给两个盒子单独设置上线margin，给其中一个设置即可。



对于嵌套的父子盒子：

```css
.father{
            width: 200px;
            height: 200px;
            background-color: green;
        }
        .son{
            width: 100px;
            height: 100px;
            background-color: red;
            margin-top: 50px;
        }
```

```html
<div class="father">
        <div class="son"></div>
    </div>
```

给子盒子设置margin，不能实现跟父盒子隔开距离，反而会让父子盒子整体跟其他元素产生了margin：

<img src="C:\Users\64296\AppData\Roaming\Typora\typora-user-images\image-20211122002404715.png" alt="image-20211122002404715" style="zoom: 50%;" />

解决方法：

1、给父盒子元素设置`padding`或者`border`

2、给父盒子元素设置`overflow: hidde`

```css
.father{
            width: 200px;
            height: 200px;
            background-color: green;
/* 1、给父盒子添加边框 */
            /* border: 1px solid black; */
/* 2、给父盒子设置内边距padding */
            /* padding: 1px; */
/* 3、根据BFC模型，设置overflow值为hidden */
            overflow: hidden;
        }
```

<img src="C:\Users\64296\AppData\Roaming\Typora\typora-user-images\image-20211122002646596.png" alt="image-20211122002646596" style="zoom:50%;" />

## 5、盒子的尺寸计算

外盒尺寸计算：

```css
空间高度= height + padding + border +margin
空间宽度= width + padding + border + margin
```

内盒尺寸计算：

```css
空间高度= height + padding + border 
空间宽度= width + padding + border
```

```css
div.test{
            width: 100px;
            height: 100px;
            border: 10px solid grey;
            padding: 10px;
            margin: 10px;
        }
```

```css
<div class="test"></div>
```

<img src="C:\Users\64296\AppData\Roaming\Typora\typora-user-images\image-20211122113851811.png" alt="image-20211122113851811" style="zoom:80%;" />

外盒宽度=100+10 *2+10 *2+10 *2 = 160px

内盒宽度= 100+10 *2+10 *2 = 140px

应用示例：

为了使得搜索的框内盒宽度为100px，且保证一定的padding，需要调整content的宽度

``` css
.searchtab{
            margin: 50px;
            height: 30px;
            /* width: 100px; */
            width: 78px;
            line-height: 30px;
            border: 1px solid grey;
            padding-left: 20px;
        }
```

```html
    <div class="searchtab">搜索</div>
```

100px = width + 1 *2 + 20   得出width= 78px

<img src="C:\Users\64296\AppData\Roaming\Typora\typora-user-images\image-20211122114406349.png" alt="image-20211122114406349" style="zoom:67%;" />

padding值不会影响盒模型大小的情况：

1、没有给元素设置宽度或者高度

2、子元素继承了父元素的宽高，子元素设置的padding不会将父元素撑大

## 6、box-sizing

使用`box-sizing`可以用来设置元素采用哪种盒模型。

```css
box-sizing: content-box|border-box
```

对于设置同样长宽、padding、border的两个盒子

```css
 div:first-child{
            width: 200px;
            height: 200px;
            background-color: rgb(194, 70, 194);
            padding: 10px;
            border: 10px solid black;
   					margin-bottom: 10px;
        }
```

```css
 div:last-child{
            width: 200px;
            height: 200px;
            background-color: rgb(194, 70, 194);
            box-sizing: border-box;
            padding: 10px;
            border:10px solid black;
        }
```

```html
    <div>content-box</div>
    <div>border-box</div>
```

`box-sizing: content-box`：将盒子设置为w3c推荐的传统盒模型，设置`padding`、`border`会撑大整个盒子。

`box-sizing: border-box`: 将盒子设置为css3新增加的盒模型，padding和margin不会把盒子撑大，width的height的值就是整个盒模型的大小。

<img src="C:\Users\64296\AppData\Roaming\Typora\typora-user-images\image-20211122154036144.png" alt="image-20211122154036144" style="zoom: 50%;" />

## 7、box-shadow

使用`box-shadow`设置盒子的阴影

```css 
box-shadow: 水平偏移 垂直偏移 模糊距离 影子尺寸(大小) 影子颜色 外/内阴影
```

其中水平偏移和垂直偏移是必填项

```css
div{
  width: 200px;
  height: 200px;
  border: 3px solid black;
  box-shadow: 2px 2px 2px 4px rgba(0,0,0,.4) inset;
    }
```



<img src="C:\Users\64296\AppData\Roaming\Typora\typora-user-images\image-20211122155824548.png" alt="image-20211122155824548" style="zoom: 50%;" />