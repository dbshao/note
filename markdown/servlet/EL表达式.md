```
<%@page pageEncoding="utf-8" %>
<!-- taglib 指令用于引入标签库<*.tld文件，一组标签>
   uri是标签库的名称（命名空间) prefix是标签的前缀 -->
<%@taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
<!doctype html>
<html>
	<head>
		<meta charset="utf-8"/>
		<title>JSTL+EL</title>
	</head>
	<body>
	    <!-- EL取值过程
	     ${user.userName}的执行过程
	     会依次从pageContext,request,session,application中
	     查找绑定名为“user"的对象，然后调用其getName()方法，等价下面的代码
	   1.User u=request.getAttribute("user");
	   2.out.println(u.getName())
	   这种繁琐的取值，转换，输出的过程都有EL表达式代劳，而且
	   El表达式更善于处理null,若没有为userName属性赋值，页面会输出“”，
	      不会输出null。若取值时，绑定名写错，页面也会输出“”
	    -->
		<h1>EL</h1>
		<p>账号:${user.userName}</p>
		<p>密码:${user["password"]}</p>
		<!-- user.getLoves()[0] -->
		<p>兴趣:${user.loves[0]}  ${user.loves[1]}</p>
		<!-- user.getCourse().getName() -->
		<p>课程名:${user.course.name}</p>
		<!-- 若取值范围都有一样的属性，若只想从request中获取
		  可以指定取值范围，若没有找到，不会查找其他范围 pageScope ,sessionScope
		  applicationScope -->
		<p>性别:${requestScope.user.sex}</p>
		<!-- 运算 -->
		<!-- 1.算术运算 -->
		<p>课时:${user.course.days+1}</p>
		<!-- 2.逻辑运算 -->
		<p>${user.userName=="cheng"&&user.password=="123" }</p>
		<!-- 3.关系运算 -->
		<p>${user.course.days>100 }</p>
		<!-- 4.判断是否为空 -->
		<p>${empty user}</p>
		
		<!-- 获取请求参数
                          若是多个值，使用${paramValues.id }-->
		 <p>ID:${param.id }</p>
		 
	 <hr/>
	 <h1>JSTL</h1>
	 <!-- if -->
	 <p>
	   <c:if test="${user.sex=='Male'}">男</c:if>
	   <c:if test="${user.sex=='FeMale'}">女</c:if>
	 </p>
	 <!-- if的第二种用法 -->
	 <!-- 通过var 申明变量  就是表达式返回的值 -->
	 <p>
	 	<c:if test="${user.sex=='Male'}" var="r">男</c:if>
	 	<c:if test="${!r}">女</c:if>
	 </p>
	 <!-- choose -->
	 <p>
	 	<c:choose>
	 		<c:when test="${user.sex=='Male'}">男</c:when>
	 		<c:otherwise>女</c:otherwise>
	 	</c:choose>
	 </p>
	 
	 <!-- forEach
	      items 属性用来指定要遍历的集合，该值可以通过EL表达式获取
	      var 属性，用来绑定每次循环对应的数据的名称
	      varStatus 属性用来声明一个变量，该变量可以获取循环相关的参数 -->
	 <p>
	 	<c:forEach items="${users}" var="u" varStatus="s">
	 		${u.userName},${s.index},${s.count}<br/>
	 	</c:forEach>
	 </p>
	 
	 <p>
	 	<c:forEach begin="${begin}" end="${end}" var="i">
	 	  ${i} ,${users[i].userName}
	 	</c:forEach>
	 </p>
	</body>
</html>
```
