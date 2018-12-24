aspect类
```
public class MyAspect {
    /*
     * 前置通知:方法运行之前增强
     * 常用于权限控制，日志记录
     * 参数 org.aspectj.lang.JoinPoint
     * 连接点对象(方法的包装对象:方法，参数，目标对象)
     * 方法名可以随便写，但配置时要一致
     * */
	public void before(JoinPoint joinPoint){
		String loginName="admin1";
		System.out.println("方法名称"+
				joinPoint.getSignature().getName());
		System.out.println("目标对象"+
				joinPoint.getTarget().getClass().getName());
		System.out.println("代理对象"+
				joinPoint.getThis().getClass().getName());
		//判断用户有没有执行方法的权限
		if(joinPoint.getSignature().getName().equals("find")){
			if(!loginName.equals("admin")){
				throw new RuntimeException("您没有权限执行方法："+
				joinPoint.getSignature().getName()+"类型为："+
				joinPoint.getTarget().getClass().getName());
			}
		}
	}
	/*
	 * 后置通知，在目标方法运行后，返回值后执行通知增强代码逻辑
	 * 参数1.连接点对象
	 * 参数2.目标方法的返回值
	 */
	public void afterReturing(JoinPoint joinPoint,Object returnVal){
		//下发短信：调用运行商的接口，短信猫
		System.out.println("--后置通知--当前下发短信的方法：" +
				"尊敬的用户，你调用的方法返回余额为："+returnVal);
		//同时可以在下发短信后，记录日志
		System.out.println("--日志记录，操作的类型为"+joinPoint.getTarget().getClass().getName()+
				           "操作的方法："+joinPoint.getSignature().getName());
		
	}
	/*
	 * 环绕通知：目标方法执行前后，都进行增强
	 * 应用场景 ，日志，事务管理
	 * 接收参数 ，ProceedingJoinpoint 可执行的连接点，特点，可以调用proceed方法
	 *         可以随时随地执行目标对象的方法，相当于目标对象的方法被执行了
	 * 必须抛出Throwable异常
	 * 
	 */
	public Object around(ProceedingJoinPoint pj) throws Throwable{
		//模拟事务管理
		//开启事务
		System.out.println("--事务开启了......");
		//执行目标对象的方法
		Object resultObject=pj.proceed();
		System.out.println("返回结果:"+resultObject);
		//提交事务
		System.out.println("--事务提交成功....");
		return resultObject;//目标方法执行返回的结果
	}
	
	/**
	 * 抛出通知，目标代码出现异常，执行通知
	 * 一般用处理异常
	 */
	public void afterThrowing(JoinPoint jp,Throwable ex){
		//一但发生异常，发送邮件或短信
		System.out.println("++管理员你好，"+jp.getTarget().getClass().getName()+
				           "的方法："+jp.getSignature().getName()+
				           "发生了异常，异常为"+ex.getMessage());
	}
	
	/*
	 * 最终通知
	 * 无论目标方法是否发生异常，最终通知都会执行，相当于finally
	 * 应用场景：释放资源
	 */
   public void after(JoinPoint jp){
	   //释放数据库连接
	   System.out.println("数据库的connection被释放了，执行的方法是："+
			       jp.getSignature().getName());
   }
```

xml配置
```
<!-- 配置切面增强 -->
	<bean id="myAspectAdvice" class="org.ks.aspect.MyAspect"/>
   <!-- 配置aop -->
   <aop:config>
   		<!-- 配置切面:通知和切入点
   		  aop:aspect  使用aspectj方式实现aop 
   		  ref：引入切面 -->
   	  <aop:aspect ref="myAspectAdvice">
   		<!-- 配置切入点 pointCut，拦截哪些bean的哪些方法 -->
   		<!--<aop:pointcut expression="bean(*Controller)" id="myPointcut"/>
   		-->
   		<aop:pointcut 
   		     expression="execution(* org.ks.controller.EmpController.find(..))" 
   		     id="myPointcut"/>   		
   		<!-- 前置通知
   		      method:切面中的对应的方法名
   		      pointcut-ref: 注入切入点，目的是让通知关联切入点-->
   		<!--<aop:before method="before" pointcut-ref="myPointcut"/>
   	  -->
   	   <!-- 后置通知
   	        returning:配置方法中参数的名字，和参数2名字保持一致 -->
   	   <!--<aop:after-returning method="afterReturing"
   	                        returning="returnVal" pointcut-ref="myPointcut"/>
   	  -->
   	   <!-- 环绕通知 -->
   	   <!--<aop:around method="around" pointcut-ref="myPointcut"/>
   	  -->
   	  <!-- 抛出通知
   	       throwing：通知中的第二个参数，异常类型的参数的名字，在运行是
   	       spring会自动将异常传给该参数 -->
   	  <!--<aop:after-throwing method="afterThrowing" throwing="ex" 
   	                      pointcut-ref="myPointcut"/>
   	  -->
   	  <!-- 最终通知 -->
   	  <aop:after method="after" pointcut-ref="myPointcut"/>
   	  </aop:aspect>
   	  
   	  
   </aop:config>
```
