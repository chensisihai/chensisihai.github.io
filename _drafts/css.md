---
layout: post
title:  "web前端总结之css基础"
categories: css 
tags:  css
---

* content
{:toc}


>说在本文前：开始尝试总结下css所包含的各种知识，才发现css太过于琐碎，知识点很多，很难一片文章就能总结的出来。css很简单，在w3school网站上看一遍css教程，做下相应的练习，就能够写出些基本的样式，可是css也很复杂，它的很多属性都值得深入研究，当然研究起来应该是很有乐趣的。所以本文也只是总结下css最核心的几个概念，以后会针对常用属性多做总结。





CSS全称为“层叠样式表 (Cascading Style Sheets)”，它主要是用于定义HTML内容在浏览器内的显示样式，如文字大小、颜色、字体加粗等。

使用CSS样式的一个好处是通过定义某个样式，可以让不同网页位置的文字有着统一的字体、字号或者颜色等。

css3就是css的第三个版本

能做什么呢？CSS3把很多以前需要使用图片和脚本来实现的效果、甚至动画效果，只需要短短几行代码就能搞定。比如圆角，图片边框，文字阴影和盒阴影，过渡、动画等。


css和html是紧密联系在一起的


元素类型

HTML 的元素可以分为两种：

块级元素（block level element）
内联元素（inline element 有的人也叫它行内元素）
两者的区别在于以下三点：

块级元素会独占一行（即无法与其他元素显示在同一行内，除非你显式修改元素的 display 属性），而内联元素则都会在一行内显示。
块级元素可以设置 width、height 属性，而内联元素设置无效。
块级元素的 width 默认为 100%，而内联元素则是根据其自身的内容或子元素来决定其宽度。





CSS代码语法：
css 样式由选择符和声明组成，而声明又由属性和值组成，如下图所示：

在CSS中也有注释语句：用/*注释语句*/来标明



CSS 样式代码插入的形式来看基本可以分为以下3种：内联式、嵌入式和外部式三种

<p style="color:red">这里文字是红色。</p>

<style type="text/css">
span{
color:red;
}
</style>


<link href="base.css" rel="stylesheet" type="text/css" />

内联样式表（标签内部）> 嵌入样式表（当前文件中）> 外部样式表（外部文件中）。



使用CSS Reset

虽然这些年来随着浏览器的迅速发展与规范的统一，浏览器特性碎片化的情况有所改善，但是在不同的浏览器之间仍然存在着很多的行为差异。而解决这种问题的最好的办法就是使用某个CSS Reset来为所有的元素设置统一的样式，保证你能在相对统一干净的样式表的基础上开始工作。目前流行的Reset库有 normalize.css, minireset以及 ress ，它们都可以修正很多已知的浏览器之间的差异性。而如果你不打算用某个外在的库，那么建议可以使用如下的基本规则:

简单方式：
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}


选择器：

标签选择器：
p{
color:red;
} 

类选择器：

<span class="setGrey">公开课</span>
.setGrey{ color: #333; }


id选择器：

<span id="setGrey">公开课</span>

```
#setGrey{
	color: #333;
}
```

类选择器和id选择器的区别：
相同点：可以应用于任何元素
不同点：

1、在一个HTML文档中，ID选择器只能使用一次，而且仅一次。而类选择器可以使用多次。
2、以使用类选择器词列表方法为一个元素同时设置多个样式， id选择器不可以这样使用

.stress{
    color:red;
}
.bigsize{
    font-size:25px;
}
<p>到了<span class="stress bigsize">三年级</span>下学期时，我们班上了一节公开课...</p>


子选择器： 使用“>” 

.food>li{border:1px solid red;}

后代选择器：
.first  span{color:red;}

总结：>作用于元素的第一代后代，空格作用于元素的所有后代。

通用选择器：

* {color:red;}

伪类选择符：允许给html不存在的标签（标签的某种状态）设置样式

a:hover{color:red;}


分组选择符： 
当你想为html中多个标签元素设置同一个样式时，可以使用分组选择符（，）

h1,span{color:red;}

相当于：
h1{color:red;}
span{color:red;}




css的继承、层叠、特殊性

CSS的某些样式是具有继承性的，

那么什么是继承呢？继承是一种规则，它允许样式不仅应用于某个特定html标签元素，而且应用于其后代。

比如下面代码：如某种颜色应用于p标签，这个颜色设置不仅应用p标签，还应用于p标签中的所有子元素文本，这里子元素为span标签。

p{color:red;}

<p>三年级时，我还是一个<span>胆小如鼠</span>的小女孩。</p>

但注意有一些css样式是不具有继承性的。如border:1px solid red;



层叠就是在html文件中对于同一个元素可以有多个css样式存在。

当有相同权重的样式存在时，会根据这些css样式的前后顺序来决定，处于最后面的css样式会被应用。


特殊性：

是因为浏览器是根据权值来判断使用哪种css样式的，权值高的就使用哪种css样式。

下面是权值的规则：

标签的权值为1，类选择符的权值为10，ID选择符的权值最高为100。例如下面的代码：

p{color:red;} /*权值为1*/
p span{color:green;} /*权值为1+1=2*/
.warning{color:white;} /*权值为10*/
p span.warning{color:purple;} /*权值为1+1+10=12*/
#footer .note p{color:yellow;} /*权值为100+10+1=111*/


重要性（少用）
，有些特殊的情况需要为某些样式设置具有最高权值，怎么办？这时候我们可以使用!important来解决。



css格式化排版：


css盒模型：

CSS中有一种基础设计模式叫盒模型，盒模型定义了Web页面中的元素中如何来解析。

CSS中每一个元素都是一个盒模型，包括html和body标签元素。在盒模型中主要包括width、height、border、background、padding和margin这些属性，而且他们之间的层次关系可以相互影响


box-sizing：

在CSS中盒模型被分为两种，第一种是w3c的标准模型，另一种是IE的传统模型，它们相同之处都是对元素计算尺寸的模型，具体说不是对元素的width、height、padding和border以及元素实际尺寸的计算关系，它们不同之处是两者的计算方法不一致，原则上来说盒模型是分得很细的，这里所看到的主要是外盒模型和内盒模型，如下面计算公式所示：

1、W3C标准盒模型
```
外盒尺寸计算（元素空间尺寸）

element空间高度＝内容高度＋内距＋边框＋外距

element空间宽度＝内容宽度＋内距＋边框＋外距

内盒尺寸计算（元素大小）

element高度＝内容高度＋内距＋边框（height为内容高度）

element宽度＝内容宽度＋内距＋边框（width为内容宽度）
```


2.IE传统下盒模型（IE6以下，不包含IE6版本或”QuirksMode下IE5.5+”）

```
外盒尺寸计算（元素空间尺寸）

element空间高度＝内容高度＋外距（height包含了元素内容宽度、边框、内距）

element宽间宽度＝内容宽度＋外距（width包含了元素内容宽度、边框、内距）

内盒尺寸计算（元素大小）

element高度＝内容高度（height包含了元素内容宽度、边框、内距）

element宽度＝内容宽度（width包含了元素内容宽度、边框、内距）

```
在CSS3中新增加了box-sizing属性，能够事先定义盒模型的尺寸解析方式，其语法规则如下：

box-sizing: content-box | border-box | inherit  （新增）

其中最为关键的是box-sizing中content-box和border-box两者的区别，他们之间的区别可以通过下图来展示，其对盒模型的不同解析：

一切应为Border-box

虽然很多初学者并不了解box-sizing这个属性，但是它确实相当的重要。而最好的理解它的方式就是看看它的两种取值:

默认值为content-box，即当我们设置某个元素的heght/width属性时，仅仅会作用于其内容尺寸。而所有的内边距与边都是在其之上的累加，譬如某个<div>标签设置为宽100，内边距为10，那么最终元素会占用120(100 + 2*10)的像素。
border-box:内边距与边是包含在了width/height之内，譬如设置了width:100px的<div>无论其内边距或者边长设置为多少，其占有的大小都是100px。
将元素设置为border-box会很方便你进行样式布局，这样的话你就可以在父元素设置高宽限制而不担心子元素的内边距或者边打破了这种限制。




css布局模型:

float

position


CSS3 伸缩布局: flex (项目中不常用，但是未来趋势)



css动画


网站： codepen

伯乐在线 
 


在网页中，元素有三种布局模型：
1、流动模型（Flow）

2、浮动模型 (Float)
3、层模型（Layer） 定位
