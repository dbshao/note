1.什么是AOP
      面向切面编程，它是一种编程思想。Aop采取横向抽取机制，取代了传统
      纵向继承体系重复性代码的编写方式（例如，性能监视、安全检查、日志记录等)
   AOP是OOP的思想延续

传统纵向代码复用
需求：执行save方法时，先向日志表中插入数据
class UserDao{
   public void save(){
     //新增插入日志的方法
     //执行保存操作
  }
}

解决方式1：
      直接在save方法的执行保存操作前，出入向日志中插入数据的代码；
      但若多个方法都需要新增插入日志的操作，则非常麻烦

解决方式2：
     将通用的功能(插入日志）写在抽象基类中，然后让需要增加通用功能的组件
  UserDao继承，使用时，调入
class abstract BaseDao{
    //插入日志
    public void writerLog(){
      //向日志中插入数据
    }
}
class UserDao extends BaseDao{
   public void save(){
     //新增插入日志的方法
     super.writerLog();
     //执行保存操作
  }
}

方式2 java不推荐使用继承的方式进行代码的复用
 缺点：代码植入，有侵入性
 
AOP 原理
 Spring AOP主要是基于动态代理技术，当spring采用aop配置后，
 spring容器返回的目标对象(需要增加代码的类的实例),实质上是spring
 利用动态代理技术生成的一个代理类型，代理类型重写原目标对象方法的功能
 在代理类中调用切面(需要代理的一些方法和增强代码)和目标对象功能
 通俗的说：基于代理思想，对原来目标对象，创建代理对象，在不修改原对象代码
        的情况下，通过代理对象，调用增强功能的代码，从而对原有业务方法进行
        增强
 

AOP本质：将共通处理逻辑和原有传统业务处理逻辑剥离，剥离后独立封装成组件
        ，之后通过配置低耦合形式切入到传统业务组件中。这样做的好处，便于日后
     修改这些共通的业务逻辑时，不会影响传统的业务逻辑（将共通逻辑和传统逻辑
   进行解耦）

AOP相关概念
Aspect(切面) :是通知和切入点的结合，通知和切入共同定义了关于切面的
              全部内容--它的功能、在何时和何地完成其功能

jionPoint(连接点):所谓连接点指的是那些被拦截到的点。
               在spring中，这些点指的是方法，因为spring只支持方法类型的连接点
pointcut(切入点):所谓切入点是指我们要对那些joinpoint进行拦截的定义
                通知定义了切面的“什么”和“何时”,切入点就定义了"何地"
advice(通知):所谓通知是指拦截到joinpoint之后要做的事情(增强的代码，即
                共通组件及作用在目标组件的时机(前置，后置...)
              通知分为前置通知，后置通知，异常通知，最终通知，环绕通知
target(目标对象） ：代理的目标对象

weaving(织入):是指把切面应用到目标对象来创建新的代理对象的过程：切面
            在指定的连接点织入的目标对象
            

切入点的表达方式
切入点：通俗的说就是往哪些组件切入
       用于指定目标组件及其方法，在spring中使用表达式表示
三种
===方法限定表达式===
execution(修饰符？ 返回类型 方法名(参数列表) throws 异常?)
//匹配UserServiceImpl的registUser方法
execution(* org.ks.cost.service.UserServiceImpl.resistUser(..))
//匹配所有load开始的方法
execution(* load*(..))
//匹配所有service包下所有类的所有方法
execution(* org.ks.cost.service.*.*(..))
//匹配所有service包及其子包所有类的所有方法     
execution(* org.ks.cost.service..*.*(..))

==类型限定表达式===
within（类型） 
//匹配UserServiceImpl类型的所有的方法
within(org.ks.cost.service.UserServiceImpl)
//匹配service包下所有类的所有的方法
within(org.ks.cost.service.*)
//匹配所有service包及其子包所有类的所有方法     
within(org.ks.cost.service..*)

==Bean名称限定表达式===
bean(id名）
//匹配id=userServiceImpl组件对象的所有方法
bean("userServiceImpl")
//匹配所有id名以service结尾的组件对象的所有的方法
bean("*service")

spring aop编程的两种方式
方式一：spring 1.2开始支持aop编程（传统springaop编程）
编程非常复杂，spring框架采用了两种动态代理实现
a\利用cglib工具包
b\利用jdkProxy api
方式二：spring2.0之后支持第三方aop框架（aspectJ）实现另一种aop编程---推荐

步骤：
1、XML
step1、确定不表对象，确定bean对象
step2、advice（通知）的编写
step3、配置切面（通知，切入点，即通知和切入点的关联）

五种通知小结
1.只要掌握Around通知类型，就可以实现其他四种通知效果
2.可以在环绕通知的方法中按如下格式编写代码：
try{
    //前置通知的代码
    Object reuslt=proceedingJoinPoint.proceed();
    //后置通知的代码
}catch（Exception e){
    //抛出通知
}finally{
    //最终通知
}
