```
@Controller
@RequestMapping("/login")
public class LoginController {
	//获取请求参数的第一种方式，使用HttpServetRequest对象
	@RequestMapping("/login1.do")
	public String checkLogin1(HttpServletRequest req){
		String username=req.getParameter("username");
		String pwd=req.getParameter("pwd");
		System.out.println("username:"+username+",pwd"+pwd);
		return "success";
	}
	@RequestMapping("/toLogin.do")
	public String login(){
		return "login";
	}
	
	//获取请求参数方式二  自动注入方法参数 
	//当表单参数与方法参数不一致时，使用@RequestParam注解
	@RequestMapping("/login2.do")
	public String checkLogin2(String username,@RequestParam("password")String pwd){
		System.out.println("ckecklogin2的方法...");
		System.out.println("username:"+username+",pwd:"+pwd);
		return "success";
	}
	
	//获取请求参数方式三 使用自动机制封装成bean传入
	@RequestMapping("/login3.do")
	public String checkLogin3(User user){
		System.out.println("checklogin3的方法....");
		System.out.println("username:"+user.getUsername()+
				          ",passwrod:"+user.getPassword());
	   return "success";
	}
	
	//向jsp页面传值方式1 使用request
	@RequestMapping("/login4.do")
	public String checkLoing4(HttpServletRequest req){
		System.out.println("ckeckLoign4的方法");
		req.setAttribute("message","welcome");
		return "success";
	}
	
	//向jsp页面传值方式2 使用session
	@RequestMapping("/login5.do")
	public String checkLoing5(HttpSession session){
		System.out.println("checkLogin5的方法");
		session.setAttribute("message","welcome!!!");
		return "success";
	}
	
	
	//向jsp页面传值方式3 使用ModelAndView
	//ModelAndView会使用request的setAtrribute方法将值传过去
	@RequestMapping("/login6.do")
	public ModelAndView ckeckLoing6(){
		System.out.println("checkLoign6的方法");
		Map<String,String> data=new HashMap<String,String>();
	    data.put("message", "welcome hahaha");
	    return new ModelAndView("success",data);
	}
	
	//向jsp页面传值方式4 使用ModelMap
	//Modelmap会使用request的setAtrribute方法将值传过去
	@RequestMapping("/login7.do")
	public String checkLoing7(ModelMap data){
		System.out.println("checklogin7的方法");
		data.put("message", "welcome hehehe");
		return "success";
	}
	
	//向jsp页面传值方式5 使用注解@ModelAttribute
	@RequestMapping("/login8.do")
	//@ModelAttribute("username")相当于
	//request.setAttribute("username",username)
	public String checkLogin8(@ModelAttribute("username")String username){
		System.out.println("checkLoing8的方法");
		return "success";
	}
```
