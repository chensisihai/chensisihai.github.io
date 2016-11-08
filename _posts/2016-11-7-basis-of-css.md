---
layout: post
title:  "web前端总结之css基础（三）"
categories: css 
tags:  css 选择器 盒模型 布局
---

* content
{:toc}


>说在本文前：开始尝试总结下css所包含的各种知识，才发现css太过于琐碎，知识点很多，很难一篇文章就能总结的出来。css很简单，在w3school网站上看一遍css教程，做下相应的练习，就能够写出些基本的样式，可是css也很复杂，它的很多属性都值得深入研究，当然研究起来应该是很有乐趣的。所以本文也只是总结下css最核心的几个概念，以后会针对常用属性多做总结。




## css基本知识

#### css的定义
CSS全称为“层叠样式表 (Cascading Style Sheets)”，它主要是用于定义HTML内容在浏览器内的显示样式，如文字大小、颜色、字体加粗等。
css3 是css的第3个版本，它在CSS2.1的基础上增加了很多强大的新功能。目前主流浏览器chrome、safari、firefox、opera、甚至360都已经支持了CSS3大部分功能。

在编写CSS3样式时，为兼容不同的浏览器可能需要不同的前缀：

| 前缀            | 浏览器         |
| ----------------|:--------------:|
| -webkit         | chrome和safari |
| -moz            | firefox        |
| -ms             | IE    		   |
| -o              | opera          |




#### css样式类型

1、  内联样式表

```html
<p style="color:red">这里文字是红色。</p>
```

2、  嵌入样式表

```html
<style type="text/css">
	span{
	color:red;
	}
</style>
```

3、  外部样式表

```html
<link href="base.css" rel="stylesheet" type="text/css" />
```

三种样式的优先级： 内联样式表（标签内部）> 嵌入样式表（当前文件中）> 外部样式表（外部文件中）。


#### css样式重置

html标签在浏览器中都有各自的默认样式，而在不同的浏览器的默认样式之间存在着差异。在设置页面时，浏览器的默认样式往往会给我们带来麻烦，影响开发效率。所以解决办法是将浏览器的默认样式去掉，进行css reset。最简单的办法就是：

```css
*{
	margin: 0;
	padding: 0;
}
```
>注意： 以上这种做法未免有些极端，项目中一般不会这么使用。可以根据自己项目的具体情况进行样式重置。现在流行使用[normalize.css](https://github.com/necolas/normalize.css/blob/master/normalize.css)统一样式的同时保留可辨识性；

关于css reset可参考下 张鑫旭大神博文：[CSS reset的重新审视 – 避免样式重置](http://www.zhangxinxu.com/wordpress/2010/04/css-reset%E7%9A%84%E9%87%8D%E6%96%B0%E5%AE%A1%E8%A7%86-%E9%81%BF%E5%85%8D%E6%A0%B7%E5%BC%8F%E9%87%8D%E7%BD%AE/)

## css选择器

#### 基础选择器


###### 标签选择器

```css
p{ color:red; } 
```

###### 类选择器

```html
<span class="set-grey">公开课</span>
```

```css
.set-grey{ color: #333; }
```

######  id选择器

```html
<span id="set-grey">公开课</span>
```

```css
#set-grey{ color: #333; }
```

###### 类选择器和id选择器的区别：

相同点：可以应用于任何元素
不同点：

1. 在一个HTML文档中，ID选择器只能使用一次，而且仅一次。而类选择器可以使用多次。
2. 使用类选择器 列表方法为一个元素同时设置多个样式， id选择器不可以这样使用
示例：

```html
<p>到了<span class="stress bigsize">三年级</span>下学期时，我们班上了一节公开课...</p>
```
```css
.stress{
    color:red;
}
.bigsize{
    font-size:25px;
}
```

###### 通用选择器

```css
* { color:red; }
```

#### 组合选择器

###### 多元素选择器

```css
h1,span{ color:red; }
```

###### 后代选择器

```css
.first  span{ color:red; }
```

###### 子选择器

```css
.food>li { border:1px solid red; }
```

>总结：>作用于元素的第一代后代，空格作用于元素的所有后代。

###### 相邻选择器 

```html
<div>
    <p>123</p>
    <p>456</p>
</div>
```

```css
p + p { 
    color: #f00;
}
```
E + F 匹配所有紧随E元素之后的同级元素



#### 同级元素选择器

```	css
p ~ ul {  background:#ff0; }
```
E ~ F 匹配任何在E元素之后的同级F元素

#### 伪类选择器

```css
a:hover{ color:red; }
```
伪类： E:link ， E:first-child， E:visited， E:active， E:focus， E:before， E:after 等

css3中的伪类：

![]({{ site.url }}/assets/i/2016-11-7-1.png)

CSS 3的反选伪类:
E:not(s)  匹配不符合当前选择器的任何元素

```css
:not(p) { border:1px solid #ccc; }
```

CSS 3中的 :target 伪类
E:target  匹配文档中特定”id”点击后的效果

#### 属性选择器

E[att^=”val”]  : 属性att的值以”val”开头的元素

E[att$=”val”]  : 属性att的值以”val”结尾的元素

E[att*=”val”]  : 属性att的值包含”val”字符串的元素


## css特性

#### 继承性

CSS的某些样式是具有继承性的，

那么什么是继承呢？继承是一种规则，它允许样式不仅应用于某个特定html标签元素，而且应用于其后代。

比如下面代码：如某种颜色应用于p标签，这个颜色设置不仅应用p标签，还应用于p标签中的所有子元素文本，这里子元素为span标签。

```css
p{color:red;}
```

```html
<p>三年级时，我还是一个<span>胆小如鼠</span>的小女孩。</p>
```

>注意:有一些css样式是不具有继承性的。如border:1px solid red;

#### 层叠

层叠就是在html文件中对于同一个元素可以有多个css样式存在。

当有相同权重的样式存在时，会根据这些css样式的前后顺序来决定，处于最后面的css样式会被应用。


#### 特殊性

是因为浏览器是根据权值来判断使用哪种css样式的，权值高的就使用哪种css样式。

下面是权值的规则：

标签的权值为1，类选择符的权值为10，ID选择符的权值最高为100。例如下面的代码：

```css
p{color:red;} /*权值为1*/
p span{color:green;} /*权值为1+1=2*/
.warning{color:white;} /*权值为10*/
p span.warning{color:purple;} /*权值为1+1+10=12*/
#footer .note p{color:yellow;} /*权值为100+10+1=111*/
```



## html的元素类型

css和html是紧密相关的，在继续了解css的盒模型之前，需要先了解下html的元素类型。html的元素可以分为三种：

1. 块状元素 
   常用块状元素： <div>、<p>、<h1>...<h6>、<ol>、<ul>、<dl>、<table>、<address>、<blockquote> 、<form>。 设置display: block 可以将元素显示为块级元素。

   它的特点：
   (1) 一个块级元素独占一行    
   (2) 元素的高度、宽度、行高以及顶和底边距都可设置。宽度在不设置时，为父容器的100%；

2. 内联元素（行内元素）
	常用的内联元素有： &lt;a&gt;、&lt;span&gt;、&lt;br&gt;、&lt;i&gt;、&lt;em&gt;、&lt;strong&gt;、&lt;label&gt;、&lt;q&gt;、&lt;var&gt;、&lt;cite&gt;、&lt;code&gt;。设置display:inline 可以将元素显示为内联元素。

	它的特点：
	(1) 和其他元素都在一行上；
	(2) 元素的高度、宽度及顶部和底部边距(margin)不可设置，宽度为内容宽度，不可改变。

	内联元素之间为何有间距问题？ 
	除非是块级元素,否则浏览器会把连续的空白看成一个空格字符来对待    

3. 内联块状元素
   内联块状元素（inline-block）就是同时具备内联元素、块状元素的特点，常用的内联块状元素有：&lt;img&gt;、&lt;input&gt;。设置display:inline-block 可以将元素显示为内联块状元素。

   它的特点：
   (1) 和其他元素都在一行上；
   (2) 元素的高度、宽度、行高以及顶和底边距都可设置



## 盒模型

CSS中有一种基础设计模式叫盒模型，盒模型定义了Web页面中的元素中如何来解析。

CSS中每一个元素都是一个盒模型，包括html和body标签元素。在盒模型中主要包括width、height、border、background、padding和margin这些属性，而且他们之间的层次关系可以相互影响

在CSS中盒模型被分为两种：

1、 W3C标准盒模型
   在浏览器中截图如下：

   ![]({{ site.url }}/assets/i/2016-11-7-2.jpg)


```
外盒尺寸计算（元素空间尺寸）

element空间高度＝内容的height＋padding＋border＋margin

element空间宽度＝内容的width＋padding＋border＋margin

内盒尺寸计算（元素大小）

element高度＝height＋padding＋border（height为内容高度）

element宽度＝width＋padding＋border（width为内容宽度）
```


2、 IE传统下盒模型（IE6以下，不包括IE6）

```
外盒尺寸计算（元素空间尺寸）

element空间高度＝height＋margin（height包含了元素内容宽度、边框、内距）

element宽间宽度＝width＋margin（width包含了元素内容宽度、边框、内距）

内盒尺寸计算（元素大小）

element高度＝height（height包含了元素内容宽度、边框、内距）

element宽度＝width（width包含了元素内容宽度、边框、内距）

```

在CSS3中新增加了box-sizing属性，能够事先定义盒模型的尺寸解析方式，其语法规则如下：

box-sizing: content-box | border-box | inherit  （新增）

其中最为关键的是box-sizing中content-box和border-box两者的区别，他们之间的区别可以通过下图来展示，其对盒模型的不同解析：


![]({{ site.url }}/assets/i/2016-11-7-3.jpg)



## 布局

#### 流布局

流布局也就是 html中的元素的位置由元素在 (X)HTML 中的位置决定
CSS 网页布局的原理,就是按照HTML代码中对象声明的顺序,以流(flow)布局的方式 来显示它。

#### 浮动布局(float)

###### float是什么？

float即为浮动，在CSS中的作用是使元素脱离正常的文档流并使其移动到其父元素的“最左边”或“最右边”。

相应名词解释：

1. 文档流：在html中文档流即为元素从上至下排列的顺序。
2. 脱离文档流：元素从正常的排列顺序被抽离。
3. 最左边/最右边：上述的移动到父元素最左和最右是指元素往左或往右移动直到碰到另一个浮动元素或父元素内容区的边界（不包括padding）。

float 属性定义元素在哪个方向浮动。以往这个属性总应用于图像，使文本围绕在图像周围，不过在 CSS 中，任何元素都可以浮动。它也经常被用来进行布局。

float的值： left | right | none | inherit

###### 浮动的本质

就是带有方位的display:inline-block 属性。

看一个示例：

```html
<div class="news">
<img src="news-pic.jpg" />
<p>some text</p>
</div>
```

```css
.news {
  background-color: gray;
  border: solid 1px black;
}

.news img {
  float: left;
}

.news p {
  float: right;
}
```
上面代码展示如下图：


![]({{ site.url }}/assets/i/2016-11-7-4.png)


这种情况下，就出现了一个问题。因为浮动元素脱离了文档流，所以包围图片和文本的 div 不占据空间。这个时候呢，就需要清浮动，使用clear属性

clear 属性规定元素的哪一侧不允许其他浮动元素。

![]({{ site.url }}/assets/i/2016-11-7-5.png)


清楚浮动方法有很多，可以参考大漠大神的博文： [Clear Float](http://www.w3cplus.com/css/clear-float)



#### 层布局（position）

position：规定元素的定位类型。任何元素都可以定位。

position可能的值：

1. static：默认值，没有定位，元素出现在正常的文档流中。
2. inherit：规定应该从父元素继承 position 属性的值。

3. fixed: 相对于浏览器窗口进行定位，并且不会随滚动条进行滚动。

4. relative：相对于其正常位置进行定位。可以给元素设置位移，仍是正常的，处于文档流中

5. absolute：绝对定位元素会脱离文档流，他是相对于它的祖先元素中设置了相对定位的最近的一个祖先元素来进行定位的，否则会相对于页面的主体进行定位。
	

盒子的位移属性有四个“top、right、bottom和left”，用来指定元素的定位位置和方向。这些属性只能在元素的“position”属性设置了“relative、absolute和fixed”属性值，才生效。


#### CSS3 伸缩布局(flex)

flex是css3 新增的一种布局方案，弹性布局。

关于弹性布局的学习可参考阮一峰博文 : [Flex 布局教程](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?utm_source=tuicool)



## css3变形与动画

参考：w3cplus： [CSS3 Transform](http://www.w3cplus.com/content/css3-transform)    [CSS动画](http://www.w3cplus.com/css3/CSS3-animation.html)
