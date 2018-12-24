1、什么是事务
事务和数据库操作有关，commit事务提交，rollback事务回滚
事务作用：保证一组和数据库有关的操作的完整性
try{
开启事务
操作1--》db操作
操作2--》db操作
操作3--》db操作
提交事务
}catch{
回滚事务
}

2、jdbc事务管理
jdbc事务管理默认提交，每执行一个executeUpdate（）方法会自动commit或出现异常rollback
若想将多个操作放在同一事物下，需要手动设置：如转账

3、Mybatis框架（单独使用）
默认没有自动提交，需要执行sqlSession.commit();

4、与spring结合
jdbc和Mybatis与spring结合，默认是一个db操作就自动提交（一个操作属于一个事务）
如果多个需要将多个操作绑定成一个整体，就需要spring事务管理（即多个操作放在同一个事务中，如转账）

spring事务管理有以下两种方式：
a\声明式事务管理（基于配置）
----注解配置（更简单，灵活，打包后（class文件），需修改，需要修改源码，分散不易管理）
----xml配置（繁琐，耦合度更低）便于维护

b\编程式事务管理（基于Java编写，TransactionTemplate）
不利于整体配置，很少使用

spring事务特性
a\读写（查 增删改）
默认可读写 readOnly=false
若只有查询，建议使用只读模式 readonly=true

b\回滚
默认运行时异常回滚，检查时异常不回滚
对于检查时异常可以通过注解和配置指明
@Transactional(rollbackFor=IOException.class)



对于自定义异常
不会回滚 需要注明roolbackFor=MyException
public class MyException extends Exception()
//回滚，建议
public class MyException extends RuntimeException()

c\传播
默认情况是REQUIRED,可以使用propagation=Propagation.类型
配置
若f1有事务，则f2使用和f1相同的事务，这样做，f1和f2在同一事务中，操作3，4出现异常，1，2会回滚，否则就给f2(3,4)创建一个事务
@Transatioanl
public void f1(){
处理1；
处理2；
f2();
}

@Transatioanl
public void f1(){
处理3；
处理4；
}

d\隔离
对相同的数据进行读写时，事务并发会发生错误数据处理，会产生脏读、幻读，不可重复读等错误，这些可以通过设置事务的隔离级别来解决
脏读：一个事务读取了另一个事务改写但还未提交的数据，如果这些数据被回滚，则读到的数据时无效的
不可重复读：在同一事务中，多次读取同一数据返回的结果不同，换句话说，后续读取可以读到另一事务已提交的更新数据，这样就会出现两次读取数据不一样(如事务t1读取某一数据，事务t2读取并修改了该数据，t1为了读取值惊醒校验而在此读取改数据，得到了不同的结果）
可重复读：在同一事务中多次读取数据时，能够保证所读数据一样，也就是后续读取不能读到另一事务已经提交更新的数据
幻读：一个事务读取了几行记录后，另一事务插入一些记录，幻读就发生了，再后来的查询中，第一个事务就会发现原来没有的记录

隔离级别（isolation）：
1、读未提交 READ_UNCOMMITTED 还未提交就能查看
2、读已提交 READ_COMMITTED 这个级别会把查看，增删改隔离开来，未提交的增删改不能查看
3、可重复读REPEATABLE_READ
4、序列化操作SERIALIZABLE 事务间对同一数据互斥，必须等第一个事物完成之后，第二个事务才可以操作
默认值 DEFAULT(oracle 默认值是第二个，mysql是第三个）
隔离级别由低到高的顺序 READ_UNCOMMITTED -->READ_COMMITTED-->REPEATABLE_READ-->SERIALIZABLE级别越高安全性越高，并发处理能力越低

@Transactional（isolation=isolation.READ_COMMITED)
public void f3(){
处理1
处理2
}

spring
一、基于注解方式实现spring声明式事务控制
step1、在主applicationContext配置如下：
<!--声明事务主键-->
<bean id="txManager" class="org.springframework.jdbc.datasource.DatasourceTransaManager“>
<!--配置数据源：告知声明事务组件需要实现事务控制的数据库-->
<property name="dataSource" ref="dataSource"/>
</bean>
<!--开启声明式事务注解扫描
开启自动代理，配置事务控制主键对象-->
<tx:annotation-driven
proxy-target-class="true"
transaction-manager="txManager"/>

step2、在方法前、类前添加注解@Transactional
添加在方法上的优先级高于类

step3、事务属性设置（不设置即为默认值）
a、propagation
事务的传播属性（默认即可）：PROPATION.REQUIRED
b、isolation
事务的隔离级别（默认）：ISOLATION.DEFAULT
c、readOnly
事务的只读模式：默认是false
d、rollback
遇到什么类型的异常，需要回滚
e、noRollback
遇到什么类型的异常不需要回滚


二、基于xml配置
step1、在主applicationContext配置如下：
<!--声明事务主键-->
<bean id="txManager" class="org.springframework.jdbc.datasource.DatasourceTransaManager“>
<!--配置数据源：告知声明事务组件需要实现事务控制的数据库-->
<property name="dataSource" ref="dataSource"/>
</bean>
step2:xml配置声明事务的范围及类型：定义通知，通知中要处理的就是事务
<tx:advice id="txAdvice" transaction-manager="txManager"/>

step3、配置事务的属性
<tx:attributes>
a、propagation
事务的传播属性（默认即可）：PROPATION.REQUIRED
b、isolation
事务的隔离级别（默认）：ISOLATION.DEFAULT
c、readOnly
事务的只读模式：默认是false
d、rollback
遇到什么类型的异常，需要回滚
e、noRollback
遇到什么类型的异常不需要回滚

<tx:method name="save" propagation="REQUIRD"
isolation="default”
readonly=“false”
rollback-for="Java.lang.IOException"/>
<!--支持通配符-->
<tx:method name="find*" />
<tx:attributes>

</tx:advice>
<!--配置切入点，让通知关联切入点-->
<aop:config proxy-target-class="true”>
<aop:pointcut
expression=""  id="txPoint">
<aop:adviso advice-ref="txAdvice" pointcut-ref="txPoint"/>
</aop>
