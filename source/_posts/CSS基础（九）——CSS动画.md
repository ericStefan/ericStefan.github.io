---
title: CSS基础（九）—— CSS动画
categories: 
- web前端
description: CSS动画
cover: https://s2.loli.net/2024/05/31/uXHVzkWREpBPxNQ.png
tags:
- css
---

# CSS动画

## 1、`transition`过渡

```css
transition: 过渡属性 过渡时间 过渡类型 延迟时间
```

过渡属性：填写要改变的属性，例如`width` `background-color`等，填写all表示元素的所有属性

过渡时间：属性改变需要的时间，必须填单位s。

过渡类型：

- **linear： (最常用)**

  线性过渡。等同于贝塞尔曲线(0.0, 0.0, 1.0, 1.0) 

- **ease：(最常用)** 

  平滑过渡。等同于贝塞尔曲线(0.25, 0.1, 0.25, 1.0) 

- ease-in： 

  由慢到快。等同于贝塞尔曲线(0.42, 0, 1.0, 1.0) 

- ease-out： 

  由快到慢。等同于贝塞尔曲线(0, 0, 0.58, 1.0) 

- ease-in-out： 

  由慢到快再到慢。等同于贝塞尔曲线(0.42, 0, 0.58, 1.0) 

- step-start： 

  等同于 steps(1, start) 

- step-end： 

  等同于 steps(1, end) 

延迟时间：在多少时间后开始执行动画，记得填单位

举例：

```css
transition: all .5s ease 0
```



## 2、`translate()`平移

x, y表示水平和垂直的平移距离，只填一个数字默认y为0。注意：正值表示向右向下移动，负值向上向右

```css
transform: translate(x,y)
```

分别表示X, Y, Z轴上的平移

```css
transform: translateX()
transform: translateY()
transform: translateZ()
```

表示三维轴上的平移：

```css
transform: translate3d(x,y,z)
```

## 3、`rotate()`旋转

用deg做单位，表示旋转多少度，正值表示顺时针，负值表示逆时针。

使用`transform-origin`属性来设置旋转轴，可以设置坐标。默认旋转轴是元素正中心。

```css
transform-origin: top right;
```

在二维平面上旋转：

```css
transform: rotate(180deg);
```

在三维轴上旋转：

```CSS
transform: rotateX();  /*以x轴方向为轴旋转*/
transform: rotateY();  /*以y轴方向为轴旋转*/
transform: rotateZ();  /*以z轴方向为轴旋转（即平面上的旋转）*/
```

自定义旋转轴，使用,其中x, y, z取值为对应方向轴的矢量（取值0-1），a表示沿着三个矢量构成旋转轴的选择量，单位为deg

```css
transform: rotate3d(x,y,z,a);
```

```css
transform: rotate3d(0.5,0.4,1,80deg)
```

## 4、`scale()`缩放

常用来实现图片悬浮放大效果

```css
transform: scale(缩放倍数);
```

## 5、`skew()`倾斜

只写一个值表示x轴倾斜，正值向左向下，复值向右向上(以左边为基准)

```css
transform: skew(0deg,20deg); 
```

``` css
transform: skewX(); /X轴方向的倾斜/
transform: skewY(); /Y轴方向的倾斜/
```

## 6、`perspective`透视距离

用这个属性可以设置透视距离，实现3d动画的效果。

```css
perspective: 1000px
```

## 7、`animation`实现动画

使用`animation`可以是动画自动执行，不需要诱发条件（比如:hover）。

属性值：

```css
animation: 动画名称  时间  过渡类型 延迟时间 循环次数 是否反向 动画状态(暂停或运动)
```

```css
animation: gogo   0.6s   ease  0s  2  normal
```

循环次数设置为：infinite  可以让动画一直执行

过渡类型有：

​		normal： 正常方向 

​        reverse： 反方向运行 

​        alternate： 动画先正常运行再反方向运行，并持续交替运行 

​        alternate-reverse： 动画先反运行再正方向运行，并持续交替运行 

**申明动画**

可用from和to来展示两个状态的变化

```css
@keyframes 动画名称 {
	form{
		transform: translate();
	}
	to{
		transform:translate();
	}
}
```

  使用百分比，来展示多个状态组成的动画 

``` css
        @keyframes 动画名称{
            0%{
                transform: translate();
            }
            25%{
                transform: translate();
            }
            50%{
                transform: translate();
            }
            75%{
                transform: translate();
            }
            100%{
                transform: translate();
            }
        }
```

可以使用`animation-play-state`来暂停动画

```css
animation-play-state: paused|running
```

