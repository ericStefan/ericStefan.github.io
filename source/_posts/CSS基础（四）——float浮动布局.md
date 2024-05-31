---
title: CSS基础（四）—— float浮动布局
categories: 
- web前端
description: css布局
cover: https://s2.loli.net/2024/05/31/6yJBxHFWtbuXUvL.png
tags:
- css
---

# css布局

## 1、正常流

block元素会单独占用一行

## 2、浮动流

`float`默认值为none

```css
float: left|right|none
```

float的特性：

1、float会使元素浮在标准流的上一层，后面的元素会根据正常流的方式来占用原来的位置，

```css
.son:first-child{
            width: 100px;
            height: 100px;
            background-color: green;
            float: left;
        }
```

```html
<div class="father">
        <div class="son">12345</div>
        <div class="son">2345</div>
    </div>
```

<img src="C:\Users\64296\AppData\Roaming\Typora\typora-user-images\image-20211123103747471.png" alt="image-20211123103747471" style="zoom:50%;" />

2、`block`和`inline`元素在设置了`float`属性后，会获得`inline-block`的特性，两个块级元素都设置`float:left`会顶对齐，未设置宽高的`block`元素宽高由内容决定，`inline`元素在浮动后宽高也能设置了。

```css
.son:first-child{
            width: 100px;
            height: 100px;
            background-color: green;
            float: left;
        }
        .son:nth-child(2){
            /* width: 150px; */
            height: 200px;
            background-color: red;
            float: left;
        }
        span{
            height: 100px;
            float: left;
            background-color: yellow;
        }
```

```html
<div class="father">
        <div class="son">12345</div>
        <div class="son">2345000000</div>
        <span>12345</span>
    </div>
```



3、浮动流的使用要和标准流搭配

```css
.son:first-child{
            width: 100px;
            height: 100px;
            background-color: green;
            /* float: left; */
        }
        .son:nth-child(2){
            width: 150px;
            height: 200px;
            background-color: red;
            float: left;
        }
```

```html
<div class="father">
        <div class="son">12345</div>
        <div class="son">2345000000</div>
    </div>
```

第一个div未设置float，按标准流排列，单独占用一行，因此第二个设置了float的div也不会跳到第一行，在页面布局中，部分需要浮动的元素，使用div嵌套会减少对其他页面组件的影响

<img src="C:\Users\64296\AppData\Roaming\Typora\typora-user-images\image-20211123105455179.png" alt="image-20211123105455179" style="zoom:33%;" />