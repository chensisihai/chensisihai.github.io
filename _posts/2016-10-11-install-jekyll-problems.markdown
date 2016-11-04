---
layout: post
title:  "安装 jekyll 遇到的那些坑儿"
categories: jekyll
tags:  jekyll
---

* content
{:toc}

## 遇到的问题1

安装jekyll时使用命令： 

```
gem install jekyll
```

报错为： 

![]({{ site.url }}/assets/i/2016-10-11-1.png)




## 解决办法

根据[http://www.haorooms.com/post/gem_not_use](http://www.haorooms.com/post/gem_not_use)提供的方法：

首先查看是否只有taobao镜像

```
gem sources -l 
```
结果我是使用的taobao镜像 ，如图

![]({{ site.url }}/assets/i/2016-10-11-2.png)


然后我尝试进行如下操作（将淘宝镜像换成rubygems）：

```
gem sources --remove https://ruby.taobao.org/
gem sources -a https://rubygems.org/
```

之后再进行安装就成功了。

## 遇到的问题 2

jekyll安装完成，启动服务 jekyll serve 时，报错：

![]({{ site.url }}/assets/i/2016-10-11-3.png)

## 解决办法

通过百度搜索，判断应该是jekyll版本兼容问题， 重新安装jekyll -v 2.4.0 ，命令如下：
```
gem uninstall jekyll
gem install jekyll -v 2.4.0
```

又遇到了如下图所示的错误：

![]({{ site.url }}/assets/i/2016-10-11-4.png)


按照 [http://blog.csdn.net/wangchong0/article/details/7408515](http://blog.csdn.net/wangchong0/article/details/7408515)  中的步骤解决。

再次安装后启动jekyll服务，但是无法访问页面。

然后仔细的查看文档，把默认配置拷贝到 _config.yml中，再次开启服务后，就可以正常访问了。

***

**有时候启动jekyll服务后 显示的服务器地址为 http://0.0.0.0:4000/ 无法打开网页，使用地址 http://localhost:4000/就可以打开了。**







