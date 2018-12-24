Spring AOP相关注解含义如下
@Aspect :用于声明切面组件
@Before：用于声明前置通知
@AfterReturing:用于声明后置通知
@After:用于声明最终通知
@Around：用于声明环绕通知
@AfterThrowing:用于声明异常通知

步骤
stept1:开启aop的注解扫描
<aop:aspectj-autoproxy proxy-target-class="true"/>
stept2:使用注解声明方面组件
