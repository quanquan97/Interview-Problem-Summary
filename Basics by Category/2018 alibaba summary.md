* 自我介绍

* 项目
你觉得你比较好的一个项目，亮点是什么，用了哪些架构？

* 具体问题
   
       1.angularjs：angularjs 的数据绑定采用什么机制？详述原理
       2.如果让你自己设计angularjs数据绑定机制， 说一下伪代码？
       3.用js实现为一个元素添加event
       4.nodejs怎么实现大文件的传输
       5.css 不知道高度的两个元素的的垂直居中排列
       6.es5，es6有了解么？
       7.es5中的bind函数，说一下
       8.反向代理的作用
       9.跨域访问

* 有什么问题想问么？


## 答案
1.脏检查机制。

双向数据绑定是 AngularJS 的核心机制之一。当 view 中有任何数据变化时，会更新到 model ，当 model 中数据有变化时，view 也会同步更新，显然，这需要一个监控。

原理就是，Angular 在 scope 模型上设置了一个 监听队列，用来监听数据变化并更新 view 。每次绑定一个东西到 view 上时 AngularJS 就会往 $watch 队列里插入一条 $watch，用来检测它监视的 model 里是否有变化的东西。当浏览器接收到可以被 angular context 处理的事件时，$digest 循环就会触发，遍历所有的 $watch，最后更新 dom。


9.跨域的产生：
同源策略限制,同源是指:域名，协议，端口相同，不同则是跨域。

1.跨域资源共享（CORS）
需要被请求方的服务端设置： Access-Control-Allow-Origin。兼容性不够好,在IE10以下的浏览器不支持。

2.服务器代理
A客户端访问A服务器，并在A服务器上做代理访问B服务器把请求结果返回A客户端，即实现了A客户端请求B服务器的跨域需求。

3.JSONP
原理:所有具有src属性的HTML标签都是可以跨域的，包括<script><img><iframe>,所以我们通常会把一些图片资源放到第三方服务器上，然后可以通过<img>标签的src属性引用。

首先在客户端注册一个callback, 然后把callback的名字传给服务器。

服务器先生成 json 数据。将 json 数据直接以入参的方式，放置到 callback中，这样就生成了一段 js 语法的文档，返回给客户端。

客户端浏览器，解析script标签，并执行返回的 javascript 代码，此时数据作为参数，传入到了客户端预先定义好的 callback 函数里.（动态执行回调函数）