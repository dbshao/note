#1、注册Servlet的访问路径
#####精确匹配（名称）
a、给Servlet取唯一的一个访问名，只能通过该访问名访问这个Servlet
b、特征：比较直观，但是比较麻烦
c、举例
查询员工：/findEmp
删除员工：/deleteEmp
新增员工：/addEmp

#####通配符（/*）
a、任何请求都可以访问这个Servlet
b、特征：可以使用一个Servlet处理项目中的所有请求
从而达到简化Servlet注册的目的
c、举例：ActionServlet —》/*
所有的请求都交给actionServlet


#####后缀（*.abc）
a、带有“abc”后缀的请求都可以访问此Servlet
b、特点：每一个模块单独使用一个Servlet处理业务，用后缀区分模块
c、举例
员工模块（增删改查员工）
EmpServlet——>*.emp
部门模块（增删改查）
DeptServlet——>*.dept
注意此方案也可以写成一个Servlet处理所有请求
即将所有请求当成一个模块
ActionServlet——>*.do

#2、项目中的做法
在项目中，为了减少web.xml的配置，通常会使用一个Servlet处理所有请求
a、参考SpringMVC框架的做法
Servlet——>*.do
即采用第三种方案（后缀）处理所有请求

b、参考Struts2框架的做法
Filter（类似于Servlet）——？/*
采用第二种方案（通配符）处理所有请求

c、注意：
①在这种方案下写Servlet，一个Servlet处理全部请求
那么必须事先约定哪个功能对应哪个请求，然后此Servlet才能遵循这个约定处理业务
②开发之前必须完成这些约定（开发规范）


##3、重构emp项目
a、目标：使用一个Servlet处理所有的请求
b、规范：
所有的请求后缀都是.do结尾
员工模块 ：查询findEmp.do
保存：saveEmp.do
删除deleteEmp.do
部门模块
查询：findDept.do
保存：saveDept.do


DAO
#####什么是DAO
data access object，封装了数据访问逻辑，调用者（一般是业务逻辑模块 ）不需要了解底层的数据访问细节就可以实现数据访问，这样一来，当底层的数据访问细节发生改变时，不会影响到调用者

EmpDaoJ dao=new EmpDaoJ(）
EmpDaoH dao=new EmpDaoH(）


如何写一个DAO
a、实体类
为了方便处理数据库中的记录，可以定义与记录对应的实体类，既可以讲数据库中的记录转成一个实体类的实例
比如Emp类，提供了id name salary age属性以及相关的get set方法，我们可以将t_emp表中的记录转换成一个Emp对象

b、dao接口
申明一些数据访问方法，这些方法不要涉及具体技术，
如：public void save(Emp e) throws SQLException；
SQLException是JDBC 中出现的异常，他涉及到了具体的技术Jdbc
可以改成：public void save(Emp e)throws Exception;

dao的实现类
采用具体的技术dao接口
如使用jdbc实现dao接口EmpdapjdbcImpl

dao工厂（工厂模式）
工厂类，封装了对象创建的细节，为调用者提供方护额要求 的对象

###重构emp项目
1、定义接口EmpDao
2、援用的EmpDao改成EmpDaoJdbcImpl，并实现Empdao接口
3、修改Servlet中的dao



















