####1、新建一个web工程项目导入相关的架包
需要导入的包大致有：


![架包](http://upload-images.jianshu.io/upload_images/66256-0ddbd3e34fb32c7f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

>其中除了spring的架包之外还包括链接mysql数据的包，EL表达式的架包，以及tomcat的一些servlet包


####2、对spring的applicationContext.xml的文件进行配置：
其中包括该项目的 异常处理和拦截过滤器，其大致配置如下
```
<util:properties id="jdbc" location="classpath:db.properties"></util:properties>

	<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource" >
		<property name="driverClassName" value="#{jdbc.driverName}"></property>
		<property name="url" value="#{jdbc.url}"></property>
		<property name="username" value="#{jdbc.userName}"></property>
		<property name="password" value="#{jdbc.password}"></property>
	</bean>

<!--配置需要扫描的项目包，一般里面包括该项目的各个组件的子包-->
	<context:component-scan base-package="netctoss"/>
	<!--配置HandleMapping-->
	<mvc:annotation-driven/>

	<bean id="viewResolver"
		  class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<property name="prefix" value="/WEB-INF/"/>
		<property name="suffix" value=".jsp"/>
	</bean>

	<!--配置系统异常解析器，处理系统异常-->
	<bean class="org.springframework.web.servlet.handler.SimpleMappingExceptionResolver">
		<property name="exceptionMappings">
			<props>
				<prop key="java.lang.Exception">error</prop>
			</props>
		</property>
	</bean>

	<!--配置拦截器-->
	<mvc:interceptors>
		<mvc:interceptor>
			<!-- 拦截的路径 -->
			<mvc:mapping path="/**"/>
			<!-- 不拦截的路径 -->
			<mvc:exclude-mapping path="/login/tologin.do"></mvc:exclude-mapping>
			<mvc:exclude-mapping path="/login/login.do"></mvc:exclude-mapping>
			<bean class="netctoss.interceptor.LinkInterceptor"></bean>
		</mvc:interceptor>
	</mvc:interceptors>

```
####3、对servlet的web.xml文件进行配置
```
  <servlet>
        <servlet-name>action</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>classpath:applicationContext.xml</param-value>
        </init-param>
        <!-- servlet容器启动之后，会立即创建DispatcherSerlvet实例
          然后调用该实例的init方法，init方法会启动spring容器，依据init-param参数
          指定位置的配置文件 -->
        <load-on-startup>1</load-on-startup>
    </servlet>

    <servlet-mapping>
        <servlet-name>action</servlet-name>
        <url-pattern>*.do</url-pattern>
    </servlet-mapping>

    <!--spring中没有进行req，resp的编码设置，需要在这里配置中文编码的问题：
配置过滤，解决中文乱码问题-->

    <filter>
        <filter-name>encodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
```

4、在entry包下写下这次业务所需要的实体类
这里就不在列出

5、在service包下写出这次业务的服务层
```

@Service
//服务层多用@service注入到springBean中
public class CostService {
//    注入需要的DAO，可以与数据库交流
    private CostDao costDao;

    public CostDao getCostDao() {
        return costDao;
    }

    @Resource(name="costDao")
//    在set方法上用@Resource实行注入，不建议在属性上注入
    public void setCostDao(CostDao costDao) {
        this.costDao = costDao;
    }

    public List<Cost> findAll(){
        return costDao.findAll();
    }
}
```
6、在controller包下写出这次业务的控制层
```
//需要在类上加上controller注解，注册bean，用equestMapping设置规划的路径
@Controller
@RequestMapping("/cost")
public class CostController {
//    注入服务业务
    private CostService costService;

    public CostService getCostService() {
        return costService;
    }

    @Resource(name="costService")
    public void setCostService(CostService costService) {
        this.costService = costService;
    }

//    规划路径
    @RequestMapping("/find.do")
    public String find(ModelMap model){
        List<Cost> list=costService.findAll();
        model.addAttribute("costs",list);
        return "cost/cost_list";
    }
}
```
