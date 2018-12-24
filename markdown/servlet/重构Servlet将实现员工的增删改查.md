```
package web;

import java.io.IOException;
import java.io.PrintWriter;
import java.util.List;


import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import Util.DAOFactory;

import Dao.EmpDAO;
import Dao.impl.EmpDAOJdbcImpl;
import entity.Emp;

public class ActionServlet extends HttpServlet {
	@Override
	protected void service(HttpServletRequest req, HttpServletResponse resp)
			throws ServletException, IOException {
		//由于该Servlet要求处理所有的请求，因此必须判断出请求的来源
		//不同的来源业务有本质的区别，请求来源看规范
		req.setCharacterEncoding("UTF-8");
		String uri=req.getRequestURI();
		String path=uri.substring(uri.lastIndexOf("/"),uri.lastIndexOf("."));
		if(path.equals("/findEmp")){
			//查询所有员工
			findEmp(req,resp);
		}else if(path.equals("/addEmp")){
			//新增员工
			addEmp(req,resp);
		}else if(path.equals("/delEmp")){
			delEmp(req,resp);
			//删除员工
		}else if(path.equals("/loadEmp")){
			//加载员工
			loadEmp(req,resp);
		}else if(path.equals("/modifyEmp")){
			//修改一个员工信息
			modifyEmp(req,resp);
		}
	}
	
	protected void findEmp(HttpServletRequest req, HttpServletResponse resp)
			throws ServletException, IOException {
		//查询 全部员工
		EmpDAO dao=(EmpDAO)DAOFactory.getInstance("EmpDao");
		List<Emp> list=dao.findAll();
		resp.setContentType("text/html;charset=UTF-8");
		PrintWriter out=resp.getWriter();
		//输出静态HTML
		//包含版本申明，根元素 head body table 等等
		
		out.println("<!DOCTYPE html>");
		out.println("<html>");
		out.println("<head>");
		out.println("<meta http-equiv='content-type' content='text/html; charset=UTF-8'>");
		out.println(" <title>员工原理列表</title>");
		out.println("</head>");
		out.println("<body>");
		
		out.println("<a href='add_emp.html'>新增</a>");
		out.println("<table width='40%' border='1px' cellspacing='0px'>");
		out.println("<tr>");
		out.println("<th>编号</th>");
		out.println("<th>姓名</th>");
		out.println("<th>薪资</th>");
		out.println("<th>年龄</th>");
		out.println("<th>操作</th>");
		out.println("</tr>");
		
		for(Emp e:list){
			out.println("<tr>");
			out.println("<td>"+e.getId()+"</td>");
			out.println("<td>"+e.getName()+"</td>");
			out.println("<td>"+e.getSalary()+"</td>");
			out.println("<td>"+e.getAge()+"</td>");
			out.println("<td><a href='delEmp.do?id="+e.getId()+"'>删除</a>" +
					"&nbsp;<a href='loadEmp.do?id="+e.getId()+"'>修改</a></td>");
			out.println("</tr>");
		}
		
		out.println("</table>");
		out.println("</body>");
		out.println("</html>");
		
	}
	
	protected void addEmp(HttpServletRequest req, HttpServletResponse resp)
			throws ServletException, IOException {
		//获取对象
		req.setCharacterEncoding("UTF-8");
		String name=req.getParameter("name");
		String salary=req.getParameter("salary");
		String age=req.getParameter("age");
		
		//封装对象
		Emp emp=new Emp();
		emp.setName(name);
		emp.setAge(Integer.parseInt(age));
		emp.setSalary(Double.parseDouble(salary));
		
		//保存
		EmpDAO dao=new EmpDAOJdbcImpl();
		dao.save(emp);
		
		//响应，输出提示信息
/*		resp.setContentType("text/html;charset=utf-8");
		PrintWriter out=resp.getWriter();
		out.println("<h1>新增成功</h1>");
		out.close();*/
		
		//修改响应改为重定向
		resp.sendRedirect("findEmp.do");
		
	}
	
	protected void delEmp(HttpServletRequest req, HttpServletResponse resp)
			throws ServletException, IOException {
		//获取参数
		req.setCharacterEncoding("UTF-8");
		String id=req.getParameter("id");
		//删除员工
		EmpDAO dao=new EmpDAOJdbcImpl();
		dao.delete(Integer.parseInt(id));
		//删除后需要 跳转到员工查询页面
		//由于员工的查询和删除是两个独立的组件，可以使用重定向
		resp.sendRedirect("findEmp.do");
	}
	
	protected void loadEmp(HttpServletRequest req, HttpServletResponse resp)
			throws ServletException, IOException {
		req.setCharacterEncoding("UTF-8" );
		String id=req.getParameter("id");
		EmpDAOJdbcImpl dao=new EmpDAOJdbcImpl();
		Emp e=dao.findById(Integer.parseInt(id));
		resp.setContentType("text/html;charset=utf-8");
		PrintWriter out=resp.getWriter();
		out.println("<form action='modifyEmp.do' method='post'>");
		out.println("<input type='hidden' name='id' value='"+e.getId()+"'></br>");
		out.println("姓名：<input  name='name' value='"+e.getName()+"'></br>");
		out.println("年龄：<input name='age' value='"+e.getAge()+"'></br>");
		out.println("薪资：<input name='salary' value='"+e.getSalary()+"'></br>");
		out.println("<input type='submit' value='确认'>");
		out.println("</form>");
		out.close();
		
				
	}

	protected void modifyEmp(HttpServletRequest req, HttpServletResponse resp)
			throws ServletException, IOException {
		req.setCharacterEncoding("UTF-8");
		Emp e=new Emp();
		e.setId(Integer.parseInt(req.getParameter("id")));
		e.setAge(Integer.parseInt(req.getParameter("age")));
		e.setSalary(Double.parseDouble(req.getParameter("salary")));
		e.setName(req.getParameter("name"));
		EmpDAOJdbcImpl dao=new EmpDAOJdbcImpl();
		dao.update(e);
		resp.sendRedirect("findEmp.do");


	}


}

```
