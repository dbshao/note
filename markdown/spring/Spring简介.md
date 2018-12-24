1.spring 是什么
  轻量级的集成开发框架
 1）轻量级
   相对于ejb,spring不依赖于应用服务器
 2）集成
    spring为软件开发提供了一套整合机制，可以将其他的一些框架（struts,hibernate)等很方便的集成进来
 3）框架
    spring 帮我们管理对象的创建和对象之间的关系
         我们可以依据spring来开发松耦合的应用程序
         
2.如何使用spring
  1.启动spring容器
    step1:创建web工程
    step2:引入spring相关的jar包
    step3:添加spring的配置文件   applicationContext.xml
    step4:写一个java类，测试
  2.使用spring容器管理对象
    1）获取对象
       注：什么是javaBean
       一个java类如果满足以下几个条件：
       有不带参的构造方法
       有属性及对应的get/set方法
       实现了序列化接口
   getBean("dog1",Dog.class)

什么事JavaBean属性
```
1.成员变量
public class Test{
//成员变量
private String n;
}

public class Test{
//属性
private String n;
public String getN（）{
return n；
}

public void setN(String n){
this.n=n;
}
}
```

>属性：是get方法中去掉get后，讲首字母小写的那个单词，上例中属性名和成员变量相同，都是n，属性名和成员变量名通常情况下相同，符合JavaBean规范

```
public class Test{
private String n;
public String getName(){
return n
}

public void setName(String name){
this.n=name
}
只读属性：只有get方法没有set方法，这种情况，我们称为只读属性
```

3.Bean的作用域
a、容器默认情况下，每一个bean的定义会创建一个对应的实例
b、作用域
singleton：单例
prototype：多例

4、延时实例化
a、Spring容器启动之后，会将所有的scope=singleton的bean实例化
b、如果设置lazy-init='true'，容器在启动时，就不会讲单例的bean实例化而是在使用的时候实例化


5、IOC（控制反转）
a、什么是IOC
指程序中的对象的获取方式发生反转，由最初的new创建，转变为第三方框架的穿件
b、什么是DI
对象之间的关系交给容器来管理
c、依赖注入方式
1）seter方式注入
容器首先调用Bean的无参构造方法创建实例，然后调用该实例的set方法来完成注入

2）构造器方法注入
容器会调用对应的构造器来完成注入

```
junit单元测试
1.右键工程--->bulidpath
2.addLibraies---->junit--->junit4
3.导入包以后，window→outline
```
