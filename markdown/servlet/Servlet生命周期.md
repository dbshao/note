> 局部变量放在栈中，实例变量放在堆中，静态变量放在方法区中

所谓生命周期，指的是Servlet容器如何创建Servlet实例，分配其资源，调用其方法，并销毁其实例的整个过程
###阶段一：实例化
创建Servlet对象，调用构造方法
在如下 两种情况下会进行对象的实例化
1、当请求到达容器时，容器查找该Servlet对象是否存在，
若存在，则直接拿来使用，不存在则创建
2、容器在启动时，或者新部署某个应用时，会检查web.xml当中Servlet是否有load-on-starup配置
如果有，则会创建改Servlet实例，load-on-up参数值越小，优先级越高（最小值为0）
Servlet 容器负责加载和实例化Servlet，当容器启动时，或者容器检测到需要这个Servlet来响应第一个请求时，web容器就加载并创建Servlet实例首先

>注意：Servlet是单例的，当容器启动或请求到达时，容器会先检测是否由此Servlet，无则创建，有则不创建，直接使用，但是对于请求Servlet引擎会为每一次请求都创建一个request和response对象

###阶段二：初始化
为Servlet分配资源，调用init方法（ServletConfig config）方法
	config对象可以用来访问Servlet的初始化参数，初始化参数通过使用init-param配置
	Servlet容器会为每一个Servlet对象创建一个ServletConfig对象


###阶段三：就绪/调用
当有请求到达容器时，容器会根据请求调用对应Servlet对象的service()方法

###阶段四：销毁
当Servlet对象初始化后就常留在内存中，直到服务器停止才需要被销毁，Servlet引擎调用Servlet对象的destroy()方法，把Servlet对象销毁

    在Servlet的整个生命周期中，init，destroy只会执行一次，而service可以执行多次。


ServletConfig接口
    创建Servlet对象时，同时会创建一个ServletConfig接口对象，ServletConfig可以为该Servlet读取预置参数，并且该对象是此Servlet对象独享，即每一个Servlet都有一个ServletConfig对象。

ServletContext对象  接口 Servlet上下文
ServletContext 是Servlet与Servlet容器之间的直接通信接口
Servlet容器在启动一个web应用时，会为他创建一个ServletContext对象，每个web应用都有唯一的一个ServletContext对象 

同一个web应用所有Servlet对象共享一个Servletcontext 
Servlet对象可以通过他来访问容器中的各种资源
Servletcontext对象在web应用被关闭时才会销毁
不同的web应用，Servletcontext各自独立

注：ServletConfig是在初始化Servlet前创建
Servletcontext是在服务器启动前创建，这两个对象都不是必须的，我们可以自己写组件给Servlet予置数据

![图片1.png](http://upload-images.jianshu.io/upload_images/66256-5b0016b9be06623e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![图片2.png](http://upload-images.jianshu.io/upload_images/66256-38cf1970835fda47.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
