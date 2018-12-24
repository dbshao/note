###基本查询语句
#####from 子句
指定从哪张表范围内查找数据
select 字段名from 表名 
查询对应字段的数据

#####where子句
where条件
根据指定条件的对查询记录进行过滤

#####select子句
select字段名 查询对应字段的数据

--查询工资大于3000的员工信息

select * from emp where salary >300
顺序是 from→where→select

###查询条件
#####使用 大于，小于，大于等于，小于等于，等于（=），不等于（！=）、不等于（<>）
#####使用and or 关键字
查询不是20部门且工资大于2000的员工信息
select *from emp where sal>2000 and deptno !=20;

>or与and优先级问题：or的优先级是最低的，如果需要提高or的优先级必须加上（）


#####使用in,not in关键字
查询20或者30部门中工资>2000的员工信息

select * from emp where deptno in (20,30) and sal >2000


#####使用like关键字
模糊查询
like不会单独使用，配合_ 或者 %一起使用
_ 表示单个匹配，%表示多个匹配
select * from emp where ename like '__A%';

#####使用 is null 和 is not null

#####使用between ……and……关键字
在两个值之间，也可以使用>=值1 and <=值2  两端都包括
select * from emp where sal between 1000 and 2000

查询81年入职的员工信息 
select * from emp where hiredate between '01-1月-81' and '31-12月-81'
select *from emp where extract(year from hiredate)=1981;

##### 使用 any、all关键字
>任意一个，>最小一个即可
<任意一个，<最大一个即可
>所有，>最大一个即可
<所有，<最小一个即可

##### 查询条件中，使用表达式和函数
 查询年薪大于30000
select* from emp where sal*12 >3000
查询工资大于30部门所有工资的员工信息
select * from emp where sal>all(select sal from emp where deptno=20);

#####使用distinct关键字
去除查询结果中重复的数据
查询员工所在的部门编号
select distinct deptno from emp

###基本sql高级组成部分
#####order by 子句
排序
在一条查询语句中，只有一次，且放在语句最后

查询20部门员工信息，按员工工资顺序排序
select * from emp where deptno=20 order by sal

asc：顺序排序关键字（默认的排序规则，asc可缺省）
desc：倒序排序关键字

#####多字段排序
order by 字段名1，字段名2……
先将结果数据按照字段1排序，再排完序的结果上，再按照字段2排序
select * from emp order by deptno ,sal desc
