######通过id注册一个bean并在class中写入改bean的Java文件，这样就注册了一个bean，scope用来规定是单例还是多例子
```
<!--bean的作用域scope默认值是singleton，单例-->
	<bean id="someBean1" class="scop.SomeBean"></bean>
	<bean id="someBean2" class="scop.SomeBean"></bean>
	<bean id="someBean3" class="scop.SomeBean" scope="prototype"></bean>

	<!--bean的生命周期回调-->
	<!--容器在创建好lifebean对象后，会调用init-method指定的方法进行初始化操作，
	容器在销毁lifebean对象时，会调用destory-method指定的方法
	lazy-init="true"：延迟加载-->
 <bean id="lifeBean" class="life.LifeBean" init-method="init" 
destroy-method="destory"
 lazy-init="true"></bean>
```
######通过ref可以对类中的非基本成员变量进行设置
```
	<bean id="dog1" class="ioc1.Dog"></bean>
	<!--<bean id="zoo" class="ioc1.Zoo">
		<property name="dog" ref="dog1"></property>
	</bean>-->
	<bean id="zoo" class="ioc1.Zoo">
		<property name="animal" ref="dog1"></property>
	</bean>
```

######在给类实例化的过程中有setter方式注入和构造器注入，setter方式注入需要类中含有setter方法，构造器注入需要类中有有参构造方法
```
<!--setter方式注入-->
	<bean id="computer" class="di.Computer">
		<property name="mainboard" value="华硕"/>
		<property name="hdd" value="希捷"/>
	</bean>

	<!--构造器注入-->
	<bean id="mobilephone" class="di.MobilePhone">
		<constructor-arg index="0" value="apple"/>
		<constructor-arg index="1" value="5000"/>
	</bean>

	<bean id="student" class="di.Student">
		<property name="computer"  ref="computer"/>
		<property name="mp" ref="mobilephone"/>
	</bean>


	<!-- 自动装配
    按照属性名自动装配，会根据属性名去查找id和属性名相同的bean，找到就自动注入
    本例中id为mp的bean，会出现null值
    因为byName，byType会出现错误，很少使用
    若改为byType时，会根据类型来找bean，但是一个类型可以对应多个实例
    到底注入哪个bean对象就不能确定了 -->
	<bean id="student1" class="di.Student" autowire="byName"></bean>
```

######当成员变量是基本值、集合、数组、spring表达式等的注入方式
```
	<bean id="computer" class="ioc2.Computer">
		<property name="mainboard" value="华硕"></property>
		<property name="hdd" value="希捷"></property>
	</bean>

	<bean id="mb1" class="ioc2.MessageBean">
		<!--注入基本值-->
		<property name="name" value="嬛嬛"></property>
		<property name="age" value="18"></property>
		<!--bean对象-->
		<property name="computer" ref="computer"></property>

		<!--注入集合-->
		<property name="langs">
			<list>
				<value>java</value>
				<value>php</value>
				<value>C</value>

				<!--若集合中的元素不是基本值，而是一个bean对象
				使用<ref bean="computer"/> value 和ref 可以混合使用-->
			</list>
		</property>

		<property name="cities">
			<set>
				<value>北京</value>
				<value>伤害</value>
				<value>广州</value>
			</set>
		</property>

		<property name="score">
			<map>
				<entry key="English" value="60"></entry>
				<entry key="Math" value="80"></entry>
				<!--若value的值是一个bean对象，可以这样写<entry key="name" value-ref="computer"/>-->
			</map>
		</property>

		<property name="dbinfo">
			<props>
				<prop key="username">scott</prop>
				<prop key="password">1234</prop>
			</props>
		</property>
	</bean>

	<!--引入方式注入集合，即将集合配置成一个bean，以达到复用的目的-->
	<util:list id="langsBean">
		<value>C++</value>
		<value>java</value>
	</util:list>

	<util:set id="citiesBean">
		<value>长沙</value>
		<value>合肥</value>
	</util:set>

	<util:map id="scoreBean">
		<entry key="English" value="90"></entry>
		<entry key="Math" value="100"></entry>
	</util:map>

	<util:properties id="dbinfoBean">
		<prop key="username">scoot</prop>
		<prop key="password">1234</prop>
	</util:properties>


	<bean id="mb2" class="ioc2.MessageBean">
		<property name="langs" ref="langsBean"></property>
		<property name="cities" ref="citiesBean"></property>
		<property name="score" ref="scoreBean"></property>
		<property name="dbinfo" ref="dbinfoBean"></property>
	</bean>

	<!--注入spring表达式-->
	<util:properties id="db" location="classpath:ioc2/db.properties">

	</util:properties>

	<bean id="someBean" class="ioc2.SomeBean">
		<property name="userName" value="#{db.userName}"></property>
		<property name="name" value="#{mb1.name}"></property>
		<property name="city" value="#{mb1.cities[0]}"></property>
		<property name="score" value="#{mb1.score.English}"></property>
	</bean>
```
