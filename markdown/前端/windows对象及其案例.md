```
<!DOCTYPE html>
<html>
  <head>
    <title>windows对象</title>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <!--<link rel="stylesheet" type="text/css" href="./styles.css">-->
    	<script type="text/javascript">
    		function f1(){
    			//打开一个新窗口
    			var win=window.open("cal.html","登陆","width=400px,height=300px");
    			setTimeout(function(){
    				win.close();
    			},5000);
    		}
    		//确认框
    		function f2(){
    			//点击确认，返回值为true，否则为false
    			var flag=confirm("确认吗");
    			if(flag){
    				alert("你选择了确认");
    			}else{
    				alert("你选择了取消 ");
    			}
    		}
    		
    		function f3(){
    			var msg=prompt("请输入手机号：");
    			alert(msg);
    		}
    		
    		function f4(url){
    			setTimeout(function(){
    			location.href=url;
    		},2000);
    		}
    	</script>

  </head>
  <body style="font-size:30px;">
  	<input type="button" value="打开窗口" onclick="f1()"/>
  	<input type="button" value="确认窗口" onclick="f2()"/>
  	<a href="deldo" onclick="return confirm('你确定删除吗')">删除</a>
  	<input type="button" value="提示窗口" onclick="f3()"/>
  </br>
  <input type="button" value="跳转到login" onclick="location.href='login.html'"/>
  <input type="button" value="跳转到QQ" onclick="f4('http://www.qq.com')"/>
   
  </body>
</html>
```

计时器案例
```
<!DOCTYPE html>
<html>
  <head>
    <title>动态时钟</title>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <!--<link rel="stylesheet" type="text/css" href="./styles.css">-->
    	<style type="text/css">
    		#p2{
    			border:1px solid red;
    			width:100px;
    			text-align:center;
    		}
    		.show{
    			display:block;
    		}
    		.hide{
    			display:none;
    		}
    	</style>
		<script type="text/javascript">
			var timer;
			var is_start=false;//是否启动
			function start(){
				if(is_start){
					return;
				}
				is_start=true;//控制一秒内多次点击
				timer=setInterval(function(){
					var now=new Date();
					var time=now.toLocaleDateString()+""+now.toLocaleTimeString();
					var c=document.getElementById("p1");
					c.innerHTML=time
				},1000)
			}
			
			function stop(){
				//如果已经暂停了就不需要暂停了
				if(!is_start){
					return;
				}
				clearInterval(timer);
				is_start=false;
			}
			
			function del(){
				//删除数据给予提示，2秒后提示消失
				var p=document.getElementById("p2");
				p.className="show";
				//2秒后关闭
				setTimeout(function (){
					p.className="hide";
				},2000)
			}
		</script>
  </head>
  
  <body>
  	<input type="button" value="启动" onclick="start();"/>
  	<button onclick="stop();">暂停</button>
  	<p id="p1"></p>
  	<hr/>
  	<button onclick="del();">删除</button>
  	<p id="p2" class="hide"> 操作成功</p>
  </body>
</html>
```
图片滚动按钮
```
<!DOCTYPE html>
<html>
  <head>
    <title>img_rol.html</title>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8">
    <!--<link rel="stylesheet" type="text/css" href="./styles.css">-->
    
    <style type="text/css">
    	.show{
    		display:block;
    	}
    	.hide{
    		display:none;
    	}
    	ul{
    		width:480px;
    		height:360px;
    		list-style-type:none;
    		padding:0px;
    	}
    </style>
    
    <script type="text/javascript">
    	var id ;
    	var count=0;//计数器
    	//开始循环轮播
    	function start(){
    		id=setInterval(function (){
    			var ul=document.getElementById("photos");
    			var lis=ul.getElementsByTagName("li");
    			for(var i=0; i<lis.length;i++){
    				lis[i].className="hide";
    			}
    			//找到要显示的li，并且显示
    			var index=count%lis.length;
    			lis[index].className="show";
    			count++;
    		},1000);
    	}
    	
    	//停止图片轮播
    	function stop(){
    		clearInterval(id);
    	}
    </script>
  </head>
  
  <body>
  <!-- onmousemove鼠标悬停事件，onmouseout鼠标撤出事件 -->
  	<ul id="photos" onmousemove="stop();" onmouseout="start();">
  		<li class="show"> <img src="../images/f1.jpg"></li>
  		<li class="hide"> <img src="../images/f2.jpg"></li>
  		<li class="hide"> <img src="../images/f3.jpg"></li>
  		<li class="hide"> <img src="../images/f4.jpg"></li>
  	</ul>
  </body>
</html>
```
