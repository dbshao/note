####中文乱码解决方案
spring提供了一个CharacterEncodingFilter过滤器，可用于解决乱码问题，在使用时，需要注意下面几点问题：
1、表单数据以post方式提交
2、在web.xml中配置CharacterEncodingFilter过滤器
3、页面编码和过滤器指定编码要保持一致
```
  <!--配置过滤，解决中文乱码问题-->

    <filter>
        <filter-name>encodingFilter</filter-name>
        <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
        <init-param>
            <param-name>encoding</param-name>
            <param-value>UTF-8</param-value>
        </init-param>
    </filter>
    <filter-mapping>
        <filter-name>encodingFilter</filter-name>
        <url-pattern>/*</url-pattern>
    </filter-mapping>
```

##验证登陆实例
>在登陆后才可以查看某些页面，否则会被转到登陆页面要求登陆

先定义一个异常：该异常继承RunTimeException
```
public class ApplicationException extends RuntimeException {
    public ApplicationException() {
        super();
    }

    public ApplicationException(String message) {
        super(message);
    }

    public ApplicationException(String message, Throwable cause) {
        super(message, cause);
    }
}
```
在服务层定义一个获得用户名的login方法：
```
    public Admin login(String adminCode,String password) {
        Admin admin=null;

            admin=adminDao.findByAdminCode(adminCode);
            if(admin==null){
                throw new ApplicationException("账户不存在");
            }
            if(!admin.getPassword().equals(password)){
                throw new ApplicationException("密码错误");
            }
           /* 异常的分类：系统异常（数据库，服务暂停，网络中断）发生之后，程序无法恢复，只能通知用户稍后重试
                    应用异常：用户的问题产生异常（输入错误的账号和密码，应提示进行正确的操作）*/

        return admin;
    }
```
在控制层做登陆控制
```
@RequestMapping("/login.do")
    public ModelAndView checkLogin(String adminCode, String password, HttpSession session){
//        try {
            Admin admin=loginService.login(adminCode,password);
            session.setAttribute("admin",admin);
/*        } catch (Exception e) {
            e.printStackTrace();
            if(e instanceof ApplicationException){
                //应用异常,提示用户
                Map<String,String> map=new HashMap<String,String>();
                //用户名回显
                map.put("adminCode",adminCode);
                map.put("message",e.getMessage());
                return new ModelAndView("login/login",map);
            }
            //系统异常，提示用户稍后尝试
            return new ModelAndView("error");
        }
        */
        //没有异常，重定向至首页
        return new ModelAndView(new RedirectView("toIndex.do"));
    }
```
若spring的配置文件中有对于异常的统一配置处理可以进行如下处理：
```
    //转发至首页
    @RequestMapping("toIndex.do")
    public String toIndex(){
        return "login/index";
    }

    @ExceptionHandler
    public String execute (HttpServletRequest req,Exception e) throws Exception {
        //应用异常，提示用户
        if(e instanceof ApplicationException){
            //回显
            req.setAttribute("adminCode",req.getParameter("adminCode"));
            req.setAttribute("message",e.getMessage());
            return "/login/login";
        }else{
//            系统异常交给Spring
            throw e;
        }
    }
```




