---
title: CSS基础（三）—— 选择器
categories: 
- web前端
description: CSS选择器
cover: https://s2.loli.net/2024/05/31/VOuDa6X5CZdzy4W.png
tags:
- css
---

# CSS选择器

## 1、关系选择器

#### 后代选择器：`.nav h3`

匹配.nav元素内所有的h3

#### 子元素选择器:`.nav>h3`

匹配.nav元素的子级h3元素

#### 相邻选择器：`.nav+h3`

选择.nav之后紧跟的h3元素

#### 兄弟选择器：`h1~h2`

选择h1之后的所有h2元素

## 2、属性选择器

#### `a[class]`

选择有class属性的a元素

#### input[type="text"]

选择所有type属性为text的input元素

#### div[class^="my"]

选择所有class属性值以my开头的div元素

#### div[class$="my"]

选择所有class属性值以my结尾的div元素

#### div[class*="my"]

选择所有class属性值包含my字符的div元素

#### div[class|="my"]

选择所有class属性值以my开头并跟着连接符“-”的div元素

#### div[class~="my"]

选择所有class属性值以空格为分隔符，其中有一个等于my的div元素

## 3、伪元素选择器

#### .fake::first-letter

选择.fake元素的第一个 字符

#### .fake::first-line

选择.fake元素的第一行

#### .fake::before

设置.fake内部之前的内容及样式（与content一起使用，这个功能可以在某个元素前增加文本和元素）

#### .fake::after

设置.fake内部之后的内容及样式（与content一起使用）

#### .fake::selection

设置.fake被选中时的样式



伪元素本质是插入一个标签元素，默认为`inline`盒子,可以对齐进行样式添加。

## 4、伪类选择器

#### h3:first-child

选择在同一层级的第一个h3

#### h3:last-child

选择同一层级的最后一个h3

### h3:nth-child(2n)

选择同一层级第2n个h3（可以设置odd/even，选择奇偶数位）

#### h3:nth-last-child(2n)

选择同一层级倒数第2n个元素

#### .nav:required

选择设置为必填的.nav类元素

#### .nav:optional

选择可选表单的.nav类元素

