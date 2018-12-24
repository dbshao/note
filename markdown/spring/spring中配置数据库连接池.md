#####配置链接Oracle数据库
```
<util:properties id="jdbc" location="classpath:db.properties"></util:properties>
	<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource"
	      destroy-method="close">
		<property name="driverClassName" value="#{jdbc.driverName}"/>
		<property name="url" value="#{jdbc.url}"/>
		<property name="username" value="#{jdbc.userName}"/>
		<prop
```
>注意class类的填写
可用如下方式获取链接
DataSource ds=ac.getBean("dataSource",DataSource.class);
		Connection conn=ds.getConnection();


配置mysql数据库
```
<util:properties id="jdbc" location="classpath:db.properties"></util:properties>
<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource" >
		<property name="driverClassName" value="#{jdbc.driverName}"></property>
		<property name="url" value="#{jdbc.url}"></property>
		<property name="username" value="#{jdbc.userName}"></property>
		<property name="password" value="#{jdbc.password}"></property>
	</bean>
```
>同样需要注意class类的填写
