####1.什么是jsp？
    sun公司制定的一种服务器端动态生成页面的技术规范
    它本质上还是Servlet

####2.jsp的组成
  1.html（css，js）
    2.java代码
	①java代码片段/jsp脚本<% %>
	②jsp表达式<%= %>
	③jsp声明<%! %>
    3.制定
	①page指令
	    import属性(导入)
	    pageEncoding属性
	    contentType属性(设置文本的类型和编码)
	    session属性 true/false  若为false，jsp就不能使用session这个隐含对象
	    isELlgnorde属性 true/false 是否忽略el表达式，若为true，忽略
	②include指令（引入文件对页面公共部分，，我们可以使用相同的jsp文件，并使用include指令导入
			如此可以实现代码的优化）
	    file属性
	③taglib指令 用于导入标签
	    uri属性 标签文件的命名空间
	    prefix属性 命名空间的前缀
    4.注释
	①<!-- --> 
	    注释中若有java代码，会执行,但不会在页面上输出
	②<%-- --%>
	    jsp中特有的注释，注释中若有java代码，会忽略

###二、jsp源文件如何转换成.java文件
    html   --> service()，使用out.write()输出
    <% %>  --> service(),照搬
    <%= %> --> service(),使用out.print()输出
    指令   --> 会影响源代码的生成，如导包
    <%! %> --> jsp声明中定义的变量回变为Servlet对应的成员变量，声明的方法会变成Servlet成员方法

###jsp隐含对象
在jsp中可以直接使用的对象，这些对象是在jsp执行前初始化的，其实是在生成service方法开头初始化的，其实是在生成service方法开头初始化 的
 #####包含九个隐含对象
a、request
HttpServletRequest
b、response
HttpServletResponse
c、out
JSPWriter==PrinterWriter
d、conf
就是ServletConfig，可以读取jsp的配置参数
e、application
ServletContext
f、exeception
Throwable是页面发生的异常，只有页面发生异常时，该对象才会有效
h、page
Object 代表页面本身
i、pageContext
是pageContext的实例，服务器会为每一个jsp实例（指的是jsp对应的那个Servlet对象创建一个唯一的一个pageContext，可以通过该实例，获取其他八个对象）

jsp隐藏对象访问范围 从小到大
pageContext 只能对应jsp实例自己可以访问，生命周期从对应的jsp对象创建到jsp对象消亡
request 一次请求能访问，生命周期在请求和响应周期
session 一次会话期间能访问，多起请求和响应期间都存在
ServletContext 整个应用内部所有的应用组件都能访问，除非服务器关闭，否则会一直存在

![隐藏对象](http://upload-images.jianshu.io/upload_images/66256-a7b00393969989fa.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![jsp-Servlet.png](http://upload-images.jianshu.io/upload_images/66256-b9015efb4dd517a7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
