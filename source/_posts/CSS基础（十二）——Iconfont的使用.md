---
title: CSS基础（十二）—— Iconfont的使用
categories: 
- web前端
description: Iconfont的使用
cover: https://s2.loli.net/2024/05/31/T3XLStMGuHzQjEi.png
tags:
- css
---


# Iconfont的使用

使用iconfont字体图标，需要先申明(以icomoon为例)

```css
@font-face {
    font-family: 'icomoon'; /*自定义字体名称*/
    src: url('fonts/icomoon.eot?kkyc2');    /*fonts/是字体文件路径*/
    src: url('fonts/icomoon.eot?kkyc2#iefix') format('embedded-opentype'),
        url('fonts/icomoon.ttf?kkyc2') format('truetype'),
        url('fonts/icomoon.woff?kkyc2') format('woff'),
        url('fonts/icomoon.svg?kkyc#icomoon') format('svg');
    font-weight: normal;
    font-style: normal;
}
```

## 使用字体方式一

```css
  span{
            font-family: "icomoon";
        }
```

```html
    <!-- 直接粘贴demo里的结构 -->
    <span></span>  
```



## 使用字体方式二

```css
div::after{
            font-family: "icomoon";
            content: "\e96c";  /*对应图表的unicode*/
            font-size: 10px;
            color: red;
        }
```

```html
<!-- 使用伪类添加unicode -->
    <div></div>
```

