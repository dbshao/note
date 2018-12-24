
![原理图](http://upload-images.jianshu.io/upload_images/66256-44c1b5404990fac3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

1)	Ajax 引擎（即 XmlHttpRequest 对象），首先为该对象注册一个监听器
 （该监听器是一个事件处理函数，对状态改变事件（readyStatechange）迚行监听）

2)	当用户对 GUI 做了某种操作（将产生对应的事件，如焦点失去事件等）

3)	一旦产生对应的事件，将触发事件处理代码

4)	在执行事件处理代码时，会调用 Ajax 引擎（XmlHttpRequest 对象）

5)	发送请求：Ajax 引擎被调用后，将独自向服务器发送请求（独立于浏览器之外）

继续其他操作：在 Ajax 引擎发送请求的同时，用户在浏览器还可以对 GUI 继续做其他操作该请求是异步请求（Ajax 引擎发送请求时，没有打断用户的操作）

6)	服务器的 web 组件对请求进行处理

7)	服务器可能会调用到数据库或者处理业务逻辑的 Java 类

8)	服务器将处理结果响应给（只返回部分数据，可以是 xml 或者文本）Ajax 引擎

9)	监听器通过 Ajax 引擎获取响应数据（xml 戒者文本）

10)	监听器对 GUI 中的数据迚行更新（局部更新，不是整个页面刷新）

在整个过程中大部分是通过 JS 实现的，响应数据可能是 xml，所以 Ajax 可以看做是多种技术的融合。





XMLHttpRequest对象的重要属性
1.onreadystatechange:注册一个监听器（也就是，绑定一个事件处理函数）
2.readystate：返回该对象与服务器通讯的状态
		返回的值是一个number类型的值，不同的值表示的含义如下：
		0（未初始化）对象以建立，尚未初始化（尚未调用open方法）
		1（初始化）对象以建立，尚未调用send方法
		2（发送数据）send方法已经调用
		3（数据传送中）已经接收到部分数据		
		4（响应结束）接受了所有的数据

3.responseTexy:获取服务器返回的文本
4.responseXML:获取服务器返回的XML，dom对象
5.status：获取状态码200,500,200
