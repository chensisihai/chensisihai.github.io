---
layout: post
title:  "css中隐藏内容方法的简单总结"
categories: css 
tags:  css 隐藏
---

* content
{:toc}


## display

```
display:none
```
不占据空间，不能点击，并且DOM可以获取




## visibility

```
visibility: hidden;
```
占据空间，不能点击

#### display 和 visibility的区别：
1. 空间占据： 
	display隐藏后不占据空间，visibility隐藏后占据空间

2. 回流与渲染： 
	display:none隐藏产生reflow和repaint(回流与重绘)，而visibility:hidden没有这个影响前端性能的问题；

3. 株连性： 
	使用display隐藏，它的子孙元素都会隐藏。 父元素使用visibility:hidden; 其子元素也会隐藏。若要其子元素显示，可对其子元素使用visibility:visible

## opacity

```
opacity:0;
```
占据空间，可以点击

## overflow

```
height:0; overflow:hidden;
```
height:0和overflow:hidden组合隐藏“失效”的条件如下：祖先元素没有position:relative/absolute/fixed声明，同时内部子元素应用了position:absolute/fixed声明。

## 定位

```
position: absolute;
top: -9999px;
left:-9999px;
```
主要原理是通过将元素的 top 和 left 设置成足够大的负数，使它在屏幕上不可见。

或者是使用
```
z-index: -1;
```
也能达到隐藏的效果，这个在项目中很有用的。

## clip-path

```
clip-path: polygon(0px 0px,0px 0px,0px 0px,0px 0px);
```
占据位置，不能点击

### 参考：
[张鑫旭：您可能不知道的CSS元素隐藏“失效”以其妙用](http://www.zhangxinxu.com/wordpress/2012/02/css-overflow-hidden-visibility-hidden-disabled-use/)

[伯乐在线](http://web.jobbole.com/86415/)
