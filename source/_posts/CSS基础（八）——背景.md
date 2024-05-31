---
title: CSS基础（八）—— 背景
categories: 
- web前端
description: CSS3背景相关属性及用法
cover: https://s2.loli.net/2024/05/31/k9MFugSmnc6i7RI.png
tags:
- css
---

# CSS3背景

#### `bacground-color`

设置背景颜色



#### `background-image`

设置背景图片

```css
background-image: url(img.jpg);
```



#### `background-repeat`

设置背景图片的平铺方式，即图片以何种方式重复平铺在容器内，默认值`repeat`

```css
background-repeat: repeat|repeat-x|repeat-y|no-repeat...
```



#### `background-position`

设置背景图片的初始位置, 有两个属性值，分别表示X轴和Y轴的位置

```css
background-position: top|bottom|left|right|center
/*当只写了其中一个轴的位置时，另一个轴上默认为center*/
```

```css
/*使用像素定位*/
background-position: 100px 50px
```

```css
/*两种方式混合*/
background-position: 100px top
```



#### `background-attachment`

设置背景的滚动方式，有三个属性值：

`fixed` 背景相对视图窗口固定，滚动滑轮背景不动

`local` 背景相对于元素的内容固定

`scroll` 背景相对元素本身固定，滚动滑轮背景跟随滚动

对于能够单独滚动的元素，设置为`scroll`，滚动当前元素，背景不会跟随滚动，此时需要设置`background-attachment`为local



#### `background-size`

设置背景图片的大小，属性值为两个像素值，或者使用保留字属性

```css
background-size: 100px;
/*建议只设置宽度，图片会等比例缩放，防止失真*/
```

```css
/*将图像缩放到跟容器一样大，会有一部分内容在容器外 */
background-size: cover;
```

```css
/*保证图像显示完整的情况下，将图像放大到最大*/
background-size: contain;
```

#### `background`

多个背景样式合并到一起写

```css
background:url(img.jpg) no-repeat fixed center 100px
```

可以同时设置多个背景：

```css
background: url(img/googleicon.png) no-repeat center, url(img/images.jpg) no-repeat right rgba(0,0,0,.3);
```

此时多个背景处于一个位置的时候会出现重叠，写在前面的覆盖后面的，因此需要在最后一个背景上面设置背景颜色，防止背景颜色覆盖了背景图片