---
layout: post
title:  "前后端分离中遇到的跨域问题"
categories: js 
tags:  js ajax CORS 跨域
---

* content
{:toc}

>从年初开始，针对web前端开发，公司开始尝试进行前后端分离。虽然晚了些，但是能够开始改变就是好的。前后分离的过程中遇到很多问题，其中之一就有跨域问题，网上的解决方案也很多，但是动手尝试后才发现有很多解决方案并不适用，最后选择了CORS（跨域资源共享）方案解决。下面详细记录下解决方式，方便以后参。




## 问题描述

当我在本地通过ajax请求公司服务器上的接口时，报错如图：

![]({{ site.url }}/assets/i/2017-5-17-1.png)

通过在网上搜索查找，在服务器端的接口脚本中加入header('Access-Control-Allow-Origin:*'); 
测试后，依然有问题，需要用到token的接口，都报登录令牌错误，如图：

![]({{ site.url }}/assets/i/2017-5-17-2.png)

## 解决办法

为什么会产生跨域问题呢？

是由于浏览器的同源策略， 同源策略的目的是为了保证用户信息的安全，防止恶意网站窃取网站数据。
何为同源？指3个“相同”： 协议相同、域名相同、端口相同

由于同源策略的存在，有三种行为受到限制：

 1. Cookie、LocalStorage 和 IndexDB 无法读取。
 2. DOM 无法获得
 3. AJAX 请求不能发送。

项目中所遇到的跨域问题是ajax请求不能发送，CORS 跨源资源分享，是W3C标准，是跨源AJAX请求的根本解决方法。

CORS允许浏览器向跨源服务器，发出XMLHttpRequest请求，从而克服了AJAX只能同源使用的限制。

前端需在ajax中打开 withCredentials 属性，

```
var xhr = new XMLHttpRequest();
xhr.withCredentials = true;
```

服务器端需指定：

```
Access-Control-Allow-Origin: http://api.bob.com
Access-Control-Allow-Credentials: true
```

需要注意的是，如果要发送Cookie，Access-Control-Allow-Origin就不能设为星号，必须指定明确的、与请求网页一致的域名。




以上都是在阮大神的博客上学到滴!!!

[1、浏览器同源政策及其规避方法](http://www.ruanyifeng.com/blog/2016/04/same-origin-policy.html)

[2、跨域资源共享 CORS 详解](http://www.ruanyifeng.com/blog/2016/04/cors.html)




