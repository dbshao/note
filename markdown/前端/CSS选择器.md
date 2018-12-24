CSS的多种引用
```
<!doctype html>
<html>
	<head>
		<meta charset="UTF-8"/>
		<title>CSS的使用</title>
		<!-- 内部样式，写在head的style元素中,次样式可以被当前页面的元素复用
		tyle="text/css”申明书写的文本类型" -->
		<style type="text/css">
		h2{
			color:blue
		}
		</style>
		<!-- 外部样式，写在.css文件中，并通过link元素引入到当前页面，此文件中的样式
		可以被多个界面所复用  rel:申明引入的文件是样式表文件， type:申明引入的内容是CSS文本
		href：申明引入的文件路径和文件-->
		<link rel="stylesheet" type="text/css" href="a.css"/>
	</head>
	
	<body>	
		<!-- 内联样式卸载元素的style属性里面，此样式无法重复使用 -->
		<h1 style="color:red">CSS的使用</h1>
		<h2>3种用法</h2>
		
		<p>1、内联样式</p>
		<p>2、内部样式</p>
		<p>3、外部样式</p>
	</body>
</html>
```

CSS的选择器
```
<doctype html>
<html>
	<head>
		<meta charset="UTF-8"/>
		<title>CSS选择器</title>
		<style type="text/css">
		/*元素选择器，可以选中页面上置顶的所有原色*/
		h3{
			color:pink;
		}
		/*类选择器，可以选中页面上所有据某某些共性的元素*/
		.male{
			color:green;
		}
		
		/*id选择器，可以选中页面上指定id的唯一元素*/
		#d1{
			font-size:40px;
		}
		/*选择器组，可以选中一组选择器所对应的的元素并集*/
		.male,h3{
			background-color:#ccc;
		}
		/*派生选择器*/
		/*后代选择器，选中子孙
		选择器1(父) 选择器2(子)*/
		p b{
		color:red;
		}
		/*子元素选择器  只选中儿子
		选择器1(父)>选择器2(子*/
		p>b{
		font-size:40px;
		}
		/*伪类选择器 选择器：伪类*/
		/*选择是否访问过的状态超链接*/
		a:visited{
			color:red;
		}
		a:link{
			color:blue
		}
		/*选中激活状态(鼠标正在点击)*/
		#btn1:active{
			background-color:red;
		}
		/*选择鼠标悬停的元素*/
		img:hover{
			width:500px;
			height:400px;
		}
		/*选中获取焦点的元素(光标参数)*/
		#t1:focus{
			background-color:yellow;
		}
		</style>
	</head>
	<body>
		<h1 class="male">程老师</h1>
		<h2 class="male">李老师</h2>
		<h3>姣姣老师</h3>
		<div id="d1">
			李老师让程老师介绍对象，
			程老师毛遂自荐
		</div>
		<p>
			北京市海定区<u><b>北三环</b></u>西甲路18号<b>中鼎大厦</b>B8
		</p>    
		<p>
			<a href="http://www.w3school.com.cn">w3c</a>
			<a href="http://www.sina.com.cn">sina</a>
		</p>
		<p>
			<input type="button" value="放大" id="btn1">
		</p>
		
		<p>
			<img src="../images/pig.png">
		</p>
		<p>
			<input type="text" id="t1">
		</p>
		
	</body>
</html>
```
CSS的border边框
```
<doctype html>
<html>
	<head>
		<meta charset="UTF-8"/>
		<title>border边框</title>
		<style type="text/css">
		/*style：
		--solid实线   dashed:虚线  dotted:点状线  double：双线 */
		/*单边设置*/
		h1{
			border-left:15px solid blue;
			border-bottom:5px double blue;
		}
		/*统一设置*/
		p{
			border:1px dashed red;
		}
		/*vverflow:内容溢出设置：
		visible：溢出，默认
		hidden：隐藏
		scroll：滚动条，无论是否超出范围都添加滚动条
		auto:根据内容判断是否加滚动条，用的很多*/
		div{
			border:1px solid red;
			width:300px;
			height:55px;
			overflow:visible;
		}
		</style>
	</head>
	<body>
	<h1>程程</h1>
	<p>娇娇老师</p>
	<div>
		故夫知效一官，行比一乡，德合一君，而征一国者，其自视也亦若此矣。
		而宋荣子犹然笑之。且举世誉之而不加劝，举世非之而不加沮，定乎内外之分，
		辩乎荣辱之境，斯已矣。彼其于世，未数数然也。虽然，犹有未树也。
		夫列子御风而行，泠然善也。旬有五日而后反。彼于致福者，未数数然也。
		此虽免乎行，犹有所待者也。若夫乘天地之正，而御六气之辩，以游无穷者，
		彼且恶乎待哉？故曰：至人无己，神人无功，圣人无名。
	</div>
	</body>
</html>
```
