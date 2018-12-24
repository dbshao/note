```
<!doctype html>
<html>
	<head>
		<meta charset="utf-8"/>
		<title>联动菜单</title>
		<script type="text/javascript">
			//预置要查询的城市
			var cities=[
				["杭州","宁波","嘉兴"],
				["南京","苏州","无锡"],
				["济南","青岛","烟台"]
				];
			function change(){
				//获取选中的省
				var s1=document.getElementById("province");
				//select.value获取下拉选项中被选中的option的value值
				//默认还是option的内容，若option的属性有value属性时，则获取
				//value属性的值
				var index=s1.value;
				
				//2.查询对应的城市
				var p_cities=cities[index-1];
				
				//3.删除已有的市
				var s2=document.getElementById("city");
				var opns=s2.children;
				//第一个请选择不需要删除
				//删除时应从后往前删除，这是因为若从前往后删除会影响
				//select对象中selectIndex的值，从而出现漏删的现象
				/*for(var i=opns.length-1;i>0;i--){
					s2.removeChild(opns[i])
				}*/
				
				//重置
				s2.innerHTML="<option>-请选择-</option>";
				
				//4.添加要查询到的市
				if(p_cities){
					for(var i=0;i<p_cities.length;i++){
						//创建option节点
						var opn=document.createElement("option");
						opn.innerHTML=p_cities[i];
						//添加节点
						s2.appendChild(opn);
					}
				}
			}
		
		</script>
	</head>
	
	<body>
	   <!-- onchange 是值改变事件 -->
		省:
		<select id="province" onchange="change();">
			<option value="0">-请选择-</option>
			<option value="1">浙江省</option>
			<option value="2">江苏省</option>
			<option value="3">山东省</option>
		</select>
		市:
		<select id="city">
			<option value="0">-请选择-</option>
		</select>
	</body>
</html>
```

自定义对象
```
<!doctype html>
<html>
	<head>
		<meta charset="utf-8"/>
		<title>自定义对象</title>
		<script type="text/javascript">
			//1.直接创建对象
			//简单，但是对象结构不方便阅读
			function f1(){
				//创建对象
				var obj=new Object();
				//为对象赋值
				obj.name="程程";
				obj.age=18;
				obj.work=function (){
					alert("我是敲代码的");
				};
				//使用对象
				alert(obj.name+","+obj.age);
				obj.work();
			}
			
			//2.使用构造器创建对象
			//麻烦，但是对象的结构可读性好
			function Teacher(name,age,work){
				this.name=name;
				this.age=age;
				this.work=work;
				this.showName=function (){alert("myName is:"+this.name)};
			}
			
			function f2(){
				var obj=new Teacher("老程",40,function(){alert("我是教育小程的..")});
				alert(obj.name+","+obj.age);
				obj.work();
				obj.showName();
			}
			
			//创建json对象
			//json是简单格式的数据对象
			//常用于异步请求中传递数据
			function f3(){
				//按照json的格式创建对象，本质上也是Object
				var  obj={"name":"小程","age":3,"work":function(){alert("我是欺负程程的");}};
				alert(obj.name+","+obj.age);
				obj.work();
			}
		</script>
	</head>
	
	<body>
		<button onclick="f1();">程程</button>
		<button onclick="f2();">老程</button>
		<button onclick="f3();">小程</button>
	</body>
</html>
```
