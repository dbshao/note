<1> 不带参数的重定向
```
        方式一：使用ModelAndView
                    return new ModelAndView("redirect:/toList");
        方式二：返回String
                    return "redirect:/ toList"; 
 ```
 <2> 带参数的重定向
```
         方式一：自己手动
 return new ModelAndView("redirect:/toList?param1="+value1+"&param2="+value2);
                    弊端：传中文可能乱码
        方式二：用RedirectAttributes类
                      使用addAttribute方法，自动给你拼接url
                      使用方法：
public String save(@ModelAttribute("form") Bean form,RedirectAttributes attr){
                          ...
                          attr.addAttribute("param", value);
                          return "redirect:/toList";
                      }
                      在toList方法中可以通过获得参数的方式获取参数
 ```
 
2、请求转发：// 转发到toList请求
 ```
<1> 不带参数的转发
        方式一：使用ModelAndView
                    return new ModelAndView("forward:/toList");
        方式二：返回String
                    return "forward:/toList"; 
 
 <2> 带参数的转发
        方式一：使用ModelAndView
                    return new ModelAndView("forward:/toList?param1="+value1+"&param2="+value2");
        方式二：返回String
                    return "forward:/ toList?param1="+value1+"&param2="+value2";
```
