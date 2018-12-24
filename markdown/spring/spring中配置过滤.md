在xml文件中需要对拦截器进行配置
```
	<mvc:interceptors>
		<mvc:interceptor>
			<!-- 拦截的路径 -->
			<mvc:mapping path="/**"/>
			<!-- 不拦截的路径 -->
			<mvc:exclude-mapping path="/login/tologin.do"/>
			<bean class="netctoss.interceptor.Link"/>
		</mvc:interceptor>
	</mvc:interceptors>
```
在src下配置拦截器的Java类
```
public class SomeInterceptor implements  HandlerInterceptor{
	/*
	 * 最后执行的方法，一般用于性能检测
	 * @see org.springframework.web.servlet.HandlerInterceptor
        #afterCompletion(javax.servlet.http.HttpServletRequest, 
javax.servlet.http.HttpServletResponse, 
java.lang.Object, java.lang.Exception)
	 */
	public void afterCompletion(HttpServletRequest arg0,
			HttpServletResponse arg1, Object arg2, Exception arg3)
			throws Exception {
		// TODO Auto-generated method stub
		System.out.println("拦截器的afterCompletion方法。。。");
		
	}
	/*
	 * 二级控制器的方法执行完毕后，但是在二级控制器将ModelAndView
	 * 对象返回给前端控制之前调用
	 */
	
	public void postHandle(HttpServletRequest arg0, HttpServletResponse arg1,
			Object arg2, ModelAndView arg3) throws Exception {
		// TODO Auto-generated method stub
		/*
		 * 可以在拦截器中修改二级控制器返回给前端控制器的ModelAndView
		 */
		//修改视图名
		//arg3.setViewName(viewName);
		//修改数据
		arg3.addObject("msg","hahahahaha");
		System.out.println("拦截器的postHandle方法...");
		
	}
	
	/*
	 * 前端控制器在调用Controller(二级控制器)
	 * 的方法之前先执行preHandle方法
	 * 若该方法返回false，则表示中断调用
	 * 否则继续向下调用
	 * Object arg2是Controller处理方法(Method)对象
	 */
	public boolean preHandle(HttpServletRequest arg0, HttpServletResponse arg1,
			Object arg2) throws Exception {
		// TODO Auto-generated method stub
		System.out.println("拦截器的preHandle方法....");
		return true;
	}

}
```
