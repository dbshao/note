1.spring mvc
  1)什么是mvc
    mvc是一种软件架构模式，核心思想是将一个软件划分成三种不同类型的模块，分别是:
    m（model模型):业务处理逻辑： 业务数据，业务处理
    v(view 视图)：用户交互(提供用户操作的界面,将数据以合适的方式展现出来）
    c(controller 控制器) 负责协调模型和视图（视图向控制器发送请求，
         控制器选择调用合适的模型来处理，模型返回的处理结果也交给控制器，有控制器
         选择相应的视图来显示)
  2)spring mvc 是什么
     spring框架提供一个mvc子框架，便于我们方便编写web应用
          在spring mvc当中，不用再写中心控制器 (ActionServlet),另外，可以方便
          地将模型(model)交给spring容器来管理
          
  3）如何使用spring mvc
     1)五大组件
       step1:请求先发送给DispatcherServlet(前端控制器）
       step2:DispatcherServlet依据HanlerMapping来调用相应
                         的Controller(模型)来处理
                        注：Controller经常会再次调用其他的javaBean来处理请求
       step3：Controller返回处理结果（封装到了ModelAndView,返回给前端控制器
       Step4：DispatcherSerlvet调用ViewResolver 来生成视图
       
       
![springMVC.png](http://upload-images.jianshu.io/upload_images/66256-8d72dc8f6d58abc1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


基于注解使用springmvc
1、创建一个web工程
2、将springmvc相关的jar添加到web-inf/lib下
3、添加搜spring配置文件，在src下复制applicationContext.xml
4、在web.xml文件中配置前段控制器dispatcherservlet
5、开发contoller，并使用@contoller来配置耳机控制器
注：与实现controller接口相比，使用@controller注解的好处
 a、非侵入式
b、可以写多个处理方法
c、不用再配置文件中进行配制了
使用@RequestMapping 来配置请求地址和controller的对应关系，该注解可以放在类上也可以放在方法上
6、编写jsp
7、配制applicationContext.xml

```
<!--启动扫描模块，扫描controller包,这样，如类上加了
	@Componet,@Controller会自动纳入spring容器管理-->
	<context:component-scan base-package="controller"></context:component-scan>

	<!--为使用@RequestMapping，相当于配置HaddleMapping-->
	<mvc:annotation-driven/>


	<!--配置视图解析器 viewResolver 负责将视图名解析成具体的 视图技术，比如解析成jsp-->
	<bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<property name="prefix" value="/WEB-INF/"></property>
		<property name="suffix" value=".jsp"></property>
	</bean>
```










