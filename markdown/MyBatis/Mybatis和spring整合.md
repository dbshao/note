虽然MyBatis可以生成Dao对象，但是他并没有放到spring容器当中
MyBatis+spring要解决的问题就是将MyBatis生成的组件（Dao）交给spring的ioc容器管理
这样才可以注入到service中 

1.SqlSessionFactoryBean ：在spring容器中创建SqlSessionFactoryBean对象
2.MapperFactoryBean ：在spring容器中创建接口的实例

Spring+MyBatis 重构netCtoss资费查询
1.搭建环境
	引入框架
	--MyBatis框架，（MyBatis，数据库驱动）
	--spring框架（涉及IOC AOP DAO MVC DBCP）
	--整合包 MyBatis-Spring.jar
	--src下添加spring主配置文件application.xml

2.配置前端控制器

3.编写实体类

4.编写mapper.xml

5.创建映射器，编写mapper接口

6.spring容器配置并测试

7.编写业务组件service
