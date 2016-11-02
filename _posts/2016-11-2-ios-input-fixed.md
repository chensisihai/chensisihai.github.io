---
layout: post
title:  "ios下input focus弹出软键盘造成fixed元素位置移位"
categories:  css
tags:  input 兼容 ios
---

* content
{:toc}

## 问题描述

公司临时分配了一个移动端的项目，涉及到在底部input框中发表评论，和聊天页面。底部input框所在navbar使用了position:fixed定位到底部，在ios的safari上显示没有问题，在微信浏览器上点击input弹出软键盘后，底部navbar的fixed失效，input元素位置移位。 如图：
  



 ![]({{ site.url }}/assets/i/2016-11-2-1.jpg =300)

## 解决办法

百度后发现这个问题在ios上很常见，bootstrap对其进行了说明：
Also, note that if you’re using a fixed navbar or using inputs within a modal, iOS has a rendering bug that doesn’t update the position of fixed elements when the virtual keyboard is triggered. A few workarounds for this include transforming your elements to position: absolute or invoking a timer on focus to try to correct the positioning manually. 


最后发现最好的解决方案是 在input focus后，直接把fixed元素变成absolute定位，而不需要浏览器自己去做处理。

css代码：

```css
.posa{
	position: absolute;
}
```
js代码：

```js
//平台、设备和操作系统
var system = {
    win: false,
    mac: false,
    xll: false,
    ipad:false
};
//检测平台
var p = navigator.platform;
system.win = p.indexOf("Win") == 0;
system.mac = p.indexOf("Mac") == 0;
//system.mac = p.indexOf("Linux") == 0;
system.x11 = (p == "X11") || (p.indexOf("Linux") == 0);
system.ipad = (navigator.userAgent.match(/iPad/i) != null)?true:false;
//判断pc端
if (system.win || system.mac || system.xll||system.ipad) {
} 
//移动端
else {
    $(document).on('focus', 'input', function () {
    	$(".zb-navbar").addClass('posa');
    });

    $(document).on('blur', 'input', function () {
        $(".zb-navbar").removeClass('posa');
    });
}
```

通过测试，以上代码可以完美解决fixed问题。
