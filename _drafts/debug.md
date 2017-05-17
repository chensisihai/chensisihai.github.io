html css js


开发者工具

console.info('ok');
console.log('ok)
console.debug('ok)
console.error('ok)


console.log('%d年%d月%d日',2016,11,14)

占位符

%d:整数
%f：浮点数
%s：字符串
%o：对象


console.group("第一组");
console.log(123);
console.log(123);
console.log(123);
console.groupEnd();

console.group("第二组");
console.log(123);
console.log(123);
console.log(123);
console.groupEnd();

console.dir(console);
显示一个对象所有的属性和方法



console.time("test");

for(var i=0; i<1000000; i++){}

console.timeEnd("test");

利用console.time()可以看代码运行的时间，从而对代码进行优化



雅虎军规:

让用户更快的打开网站， 35条


1、尽可能的减少http请求

什么是减少http请求？

从客户端到服务器端的请求信息

打开网页时所看到的的文字、图片、多媒体等内容都是从服务器获取的，每一个内容的获取，就是一个http请求

合并图片
合并css文件
合并js文件

2、使用CDN（内容分发网络）

什么是CDN？
从离你最近的副本服务器上获取内容，速度更快

3、添加Expire/Cache-Control头
Cache-Control（负责控制页面的缓存机制）


4、启用Gzip压缩

把文件放到服务器进行压缩，然后再传输
，传输完后，浏览器会对传输内容解压缩再执行。

压缩将体积变小


5、将css文件放到最上面

否则页面会出现空白或闪烁

6、将script放在页面最下面

DOM加载顺序： 读取html标签，head标签
meta title  style link script  body div img 
页面初始化完毕

阻止下面代码的执行

js放到最上面，如果有死循环，就不会再往下执行了，时间长了会导致浏览器崩溃，再就是页面会长时间空白，让用户一直等待

6、避免在css中使用expressions

css expressions 俗称css表达式：把css属性和js表达式关联起来，是动态设置css属性的强大（但危险）方法。

如例子：ul a {width: expression(this.offsetWidth > 750 ? function1() : function2() );} 

表达式的问题在于它的计算频率要比我们想象中的多，当页面显示和缩放时， 页面滚动时，移动鼠标时，都会重新计算一次表达式。给css表达式增加一个计数器可以跟踪表达式的计算频率。轻松移动鼠标都能达到10000次以上的计算量，严重影响页面性能，应避免使用。






7、把js和css放到外部文件中

单独提取：

提高了js和css的复用性
减小页面体积
提高了js和css的可维护性

增加了请求数（可通过缓存解决）



写在页面内：
减少页面请求
提升页面渲染速度

不利于维护、复用



实际工作中应该按照实际情况使用

某个脚本或样式：
只应用与一个页面
不经常被访问到
脚本和样式很少


9、减少DNS查询


10、压缩js和css


11、避免重定向

用户想访问的页面A被重新指向了页面B

重定向状态吗：
1、301：永久重定向 
用户请求的页面，被移动到了另外的位置


2、302 ：临时重定向

用户请求的页面被找到了，但不在原始位置


为什么避免重定向？

增加了浏览器到服务器的往返次数

12、移除重复的脚本

13、配置实体标签（Etag）

Entity Tag 属于http协议，收web服务支持


14、使用ajax缓存





网站性能评分工具： ySlow