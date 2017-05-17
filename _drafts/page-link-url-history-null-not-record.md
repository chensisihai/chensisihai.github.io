---
layout: post
title:  "返回上一页，页面跳转时跳转历史URL不记录"
categories: js 
tags:  js 返回上一页
---

* content
{:toc}

## 问题说明

   最近在做一个移动端项目，遇到一个用户体验问题，如图：

   ![]({{ site.url }}/assets/i/2017-4-20-1.jpg)

   从个人中心页面进入到订单页面后，头部不同订单状态可以切换，都是直接的链接，当在订单状态之间反复切换时，我们在点击左上角返回按钮时，发现返回很多次还是处于订单页面，体验不好，应该直接返回到个人中心页面。 需要解决的问题是，在订单状态切换时，URL地址不要进入历史URL堆栈。


## 解决办法

   这个问题存在有几天的时间了，一直没有思路，今天无意中发现张鑫旭老师的博客中正好有解决这一问题的方案。大神真的是大神，由衷的给点个赞。用了大神的办法就把问题解决了，在此作下总结。
	

   返回上一页功能实现：
	```
   javascript:history.go(-1) // 直接返回当前页的上一页，数据全部消息，是个新页面
   javascript:history.back() // 也是返回当前页的上一页，不过表单里的数据全部还在
	```

	其他
	```
	window.location.reload() //刷新
	window.history.go(1) //前进
	window.history.forward() //前进
	```

	```
	document.referrer //JS获取上一访问页面URL地址
	```

	如果浏览器没有上一页来源信息，点击返回按钮是没有反应的，体验很奇怪。属于细节问题了，张大神也给出了解决方案，如下：
	
	左上角返回按钮的代码：
	```
	<a href="javascript:history.go(-1)" class="header-back jsBack">返回</a>
	```
	然后，
	```
	if (document.referrer === '') {
	    // 没有来源页面信息的时候，改成首页URL地址
	    $('.jsBack').attr('href', '/');
	}
	```

	无法获得上一页referrer信息的场景

	1. 直接在浏览器地址栏中输入地址；
	2. 使用location.reload()刷新（location.href或者location.replace()刷新有信息）；
	3. 在微信对话框中，点击链接进入微信自身的浏览器；
	4. 扫码进入QQ或者微信的浏览器；
	5. 直接新窗口打开一个页面；
	6. 从https的网站直接进入一个http协议的网站（Chrome下亲测）；
	7. a标签设置rel="noreferrer"（兼容IE7+）；
	8. meta标签来控制不让浏览器发送referer；
		```
		<meta content="never" name="referrer">
		```
	
	```
	location.replace(newURL)
	```
	replace() 方法不会在 History 对象中生成一个新的记录。当使用该方法时，新的 URL 将覆盖 History 对象中的当前记录。

	history.replaceState()是用来修改当前的history实体而不是创建一个新的.
	该方法可参考：[http://www.zhangxinxu.com/wordpress/2013/06/html5-history-api-pushstate-replacestate-ajax/](http://www.zhangxinxu.com/wordpress/2013/06/html5-history-api-pushstate-replacestate-ajax/)

#### 页面链接跳转历史URL不记录的兼容处理解决方案

```
var fnUrlReplace = function (eleLink) {
    if (!eleLink) {
        return;
    }
    var href = eleLink.href;
    if (href && /^#|javasc/.test(href) === false) {
        if (history.replaceState) {
            history.replaceState(null, document.title, href.split('#')[0] + '#');
            location.replace('');
        } else {
             location.replace(href);
        }
    }
};
```
要想实现最终的效果，还需要和事件关联。举个简单的例子，假设页面上有个<a>链接，希望点击的时候不进入历史记录堆栈，则可以这样：
```
document.getElementsByTagName('a')[0].onclick = function (event) {
    if (event && event.preventDefault) {
        event.preventDefault();
    }
    fnUrlReplace(this);
    return false;
};
```


参考链接：
[http://www.zhangxinxu.com/wordpress/2017/02/js-page-url-document-referrer/](http://www.zhangxinxu.com/wordpress/2017/02/js-page-url-document-referrer/)

[http://www.zhangxinxu.com/wordpress/2017/02/page-link-url-history-null-not-record/](http://www.zhangxinxu.com/wordpress/2017/02/page-link-url-history-null-not-record/)