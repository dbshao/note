```
<!doctype html>
<html>
	<head>
		<meta charset="utf-8"/>
		<title>定时器</title>
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
	</head>
	<script type="text/javascript">
	    var timer;
	    var is_start=false; //是否启动
		function start(){
	    	    if(is_start){
	    	    	return;
	    	    }
	    	    is_start=true;//控制1秒内多次点击
			    timer=setInterval(function(){
			   
				var now=new Date();
				var time=now.toLocaleDateString()+" "+now.toLocaleTimeString();
				var c=document.getElementById("p1");
				c.innerHTML=time;
			},1000);
		}
		
		function stop(){
			//如果已经暂停，就不需要再暂停了
			if(!is_start){
				return;
			}
			clearInterval(timer);
			is_start=false;
		}
	
		function del(){
			//删除数据，给予提示，2秒后，提示消失
			var p=document.getElementById("p2");
			p.className="show";
			//2秒后关闭
			setTimeout(function(){
				p.className="hide";
			},2000);
		}
	</script>
	
	<body>
		<input type="button" value="启动" onclick="start();"/>
		<button onclick="stop();">暂停</button>
		<p id="p1"></p>
		<hr/>
		<button onclick="del();">删除</button>
		<p id="p2" class="hide" >操作成功</p>
	</body>
</html>
```
