####什么是servlet
servlet是sun公司制定的一种用于扩展web服务器功能的组件规范
功能扩展：早期的web服务器只能处理静态资源，即事先写好html放在服务器上，不能生成动态的html（通过计算生成一个新的html），所谓扩展，就是让web服务器能够生成动态页面，servlet会动态处理客户的请求，并生成响应，响应的内容可以是文本，比如html xml 也可以是图片等其他格式的资源

######1、扩展服务器的功能
扩展方式一：CGI
CGI程序有两个问题：
  a 开发人员需要处理请求的参数，编程想当复杂
b程序的移植性差
扩展方式二：sevlet（组件+容器）
当请求到达web服务器时，web服务器负责处理网络相关的问题（如负责从http请求数据包中分析出请求参数），servlet只需要处理业务逻辑，另外，servlet是一个规范，可以在不同的web服务器中运行，可移植性好
######2、关于组件规范
 组件：符合规范实现了特定的功能，并且可以部署到容器上的软件模块，它不能单独运行，必须要依赖容器才能运行
容器：（tomcat ，weblogic，jboss等等）
符合规范，为组件提供运行环境，并且管理组件的生命周期（组件的加载，实例化，调用其方法，销毁的过程）

采用容器+组件的编程模式的优势：
容器负责大量的基础服务（包括浏览器与服务器之间的网络通讯，多线程，参数传递等等），组件只需要处理业务逻辑，另外，组件的运行不依赖与特定容器

Servlet访问静态和动态资源
①、如何访问静态页面？
    a、服务器上部署html
    b、浏览器访问服务器的html
②、如何访问动态页面?
    a、服务器上部署Servlet
    b、浏览器访问Servlet，由Servlet动态生成html
③、Servlet
    a、Servlet是服务器端满足规范的组件（类）
    b、它可以处理http协议，动态生成html
名词解释：
    1、部署：
	a、就是把编译后代码拷贝到tomcat/webapps下
	b、部署是专业的说法
    2、服务器
	Tomcat是服务器，也叫Java web服务器，又叫web服务器，还叫Servlet服务器

二、Tomcat的安装
    ①、window →preference →MyEclipse →Service →Tomcat →Tomcat7
    ②、将Tomcat选项置为Enable
    ③、找到tomcat的解压路径，填写tomcat base directory，自动生成tomcat temp directory
    ④、回到工具栏上的"run/sotp/restart MyEclipse Servers"图标旁边的下拉箭头 选择tomcat7.x ，点击start
    ⑤、启动浏览器，访问http://localhost:8080 测试能否正确访问


建议：tomcat7下的lauch改为Run mode，其他地方可改可不改。


三、servlet开发步骤
1、创建web项目
2、写servlet
3、注册servlet
4、使用MyEclipse启动tomcat
5、使用MyEclipse部署项目
    a、点击工具栏deploy MyEclipse j2ee project to servlet 按钮
  b、弹出对话框project deployment 
c、点击add按钮 弹出 new deployment 对话框 选择 tomcat 7.x点击 finish 弹出对话框，点击OK

6、访问servlet
7、使用MyEclipse关闭tomcat




![未标题-1.png](http://upload-images.jianshu.io/upload_images/66256-d81fc0fb65dc71ea.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
