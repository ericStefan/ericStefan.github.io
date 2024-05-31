---
title: CSS基础（十）—— 优先级
categories: 
- web前端
description: CSS优先级
cover: https://s2.loli.net/2024/05/31/Yf8XQbTq6pMxJzF.png
tags:
- css
---

# CSS优先级

## 1、css的继承性

由于css的继承性，`<p>`标签会继承`<div>`的样式

```css
div{
  color: red;
}
```

```html
<div>
  <p>你好</p>
</div>
```

## 2、CSS选择器的优先级

标签 < 类/伪类/伪元素/属性选择 < ID < 行内样式 < !important

```css
div{
  color: red;
}
#test{
  /*最后显示结果是绿色，id选择器的优先级高于属性选择器*/
  color: green;
}
div[class="nav"]{
  color: blue;
}
```

```html
<div class="nav" id="test">
  <p>这是什么颜色</p>
</div>
```

## 3、优先级的叠加性

我们假设行内样式>ID>类/伪类/属性>标签 的优先级用一个四位的数表示，行内样式在最高一位即`10000`, ID选择器为`0100`, 类选择器为`0010`, 标签选择器为`0001`。

当多个选择器同时使用的时候，优先级会进行叠加。

```css
.c1 .c2 div{
            color: blue;
        }
        #box1{
            /* 继承性权重为0 */
            color: black!important;
        }
        div #box3{
            /* 权重为0 0 0 1 + 0 1 0 0 */
            color: green;
        }
        #box1 div{
            /* 权重为0 1 0 0 + 0 0 0 1 */
          /*结果显示黄色*/
            color: yellow;
        }
        /* div #box3和#box1 div拥有相同的优先级，此时根据css的层叠性，就近原则，展示后面的样式*/
```

```html
<div id="box1" class="c1">
        <div id="box2" class="c2">
            <div id="box3" class="c3">
                这段文字是什么颜色的？
            </div>
        </div>
    </div>
```

