---
layout: post
title:  "web前端总结之开发工具Sublime Text3（一）"
categories:  开发工具
tags:  开发工具 sublime html
---

* content
{:toc}

开始做前端开发已经有一年之久了，也应该对这段时间所学做个总结了。

作为一名开发者，用一个体积轻巧，顺手工具，对工作效率的提高有极大的帮助，我最喜欢的一款工具便是Sublime Text3，一款性感的编辑神器。




Sublime Text：一款具有代码高亮、语法提示、自动完成且反应快速的编辑器软件，不仅具有华丽的界面，还支持插件扩展机制。

## Sublime Text的安装

首先在sublime官网下载软件 [https://www.sublimetext.com/3](https://www.sublimetext.com/3)

sublime安装好之后，需要安装package controll组件，以便我们通过它来安装插件。

### 安装方法：
使用ctrl+`快捷键 或 通过View-> Show Console打开控制台，粘贴如下代码：

```
import urllib.request,os,hashlib; h = 'df21e130d211cfc94d9b0905775a7c0f' + '1e3d39e33b79698005270310898eea76'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```
注意：sublime text3粘贴的是上面的代码，sublime text2不是

如果顺利的话，此时就可以在Preferences菜单下看到Package Settings和Package Control两个菜单了。

#### 如果因为某种原因没有安装成功需要手动安装，方法如下：
1. 点击Preferences > Browse Packages菜单
2. 进入打开的目录的上层目录，然后再进入Installed Packages/目录
3. 下载[Package Control.sublime-package](https://sublime.wbond.net/Package%20Control.sublime-package)并复制到Installed Packages/目录
4. 重启Sublime Text。

参考：[https://packagecontrol.io/installation#st3](https://packagecontrol.io/installation#st3)

## 我常用的插件


1. **HTML/CSS/JS Prettify**
   格式化html、css、js三种文件类型的插件，该插件依赖于node.js 。 安装此插件后，用快捷键ctrl+shift+H 完成当前文件的格式化。

2. **Emmet**
	Emmet (前身为 Zen Coding),是一种快速编写html的方法， 是一个能大幅度提高前端开发效率的一个工具

3. **LiveReload**
    可以在浏览器中实时预览。在chrome浏览器中也需要安装liveReload插件

4. **LESS2CSS**
	当保存less文件的时候自动生成同名的css文件，有错误会提示编译错误信息

5. **ConvertToUTF8**
	解决中文乱码问题


#### 插件安装方法： 
1. ctrl+shift+p 调出命令面板
2. 输入install 调出 Install Package 选项并回车，然后在列表中选中要安装的插件。



## Snippets（代码片段）功能

在编写代码时，会经常遇到一些需要反复使用的代码片段，就需要反复的复制粘贴，大大影响效率，使用snippet就能很好的解决这个问题。

创建方法：Tools > New Snippet

这时会看到如下示例代码

```
<snippet>
	<content><![CDATA[
Hello, ${1:this} is a ${2:snippet}.
]]></content>
	<!-- Optional: Set a tabTrigger to define how to trigger the snippet -->
	<!-- <tabTrigger>hello</tabTrigger> -->
	<!-- Optional: Set a scope to limit where the snippet will trigger -->
	<!-- <scope>source.python</scope> -->
</snippet>
```
相对应的完整结构：

```
<snippet>
    <content><![CDATA[ 
    //你需要插入的代码片段${1:name} 
    ]]></content>
    <!-- 可选：快捷键，利用Tab自动补全代码的功能 -->
    <tabTrigger>chen-snippet</tabTrigger>
    <!-- 可选：使用范围，不填写代表对所有文件有效。附：source.css和test.html分别对应不同文件。 -->
    <scope></scope>
    <!-- 可选：在snippet菜单中的显示说明（支持中文）。如果不定义，菜单则显示当前文件的文件名。 -->
    <description>My Fancy Snippet</description>
</snippet>
```
根据以上结构进行创建，创建完毕以后，保存在\Packages\User目录下（例 X:\Sublime Text 3\Data\Packages\User），文件命名为xx-code，后缀名.sublime-snippet。

打开html文件，输入chen-snippet， 再按tab键，所编写的代码片段，就插入进来了。


## 快捷键

可参考： [http://blog.csdn.net/cywosp/article/details/31791881](http://blog.csdn.net/cywosp/article/details/31791881)