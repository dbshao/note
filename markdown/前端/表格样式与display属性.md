表格样式：
```
<!doctype html>
<html>
	<head>
		<meta charset="UTF-8"/>
		<title>表格样式</title>
		<style type="text/css">
			table{
				border: 1px solid red;
				width:300px;
				padding:10px;
				/*边框和边框的距离
				border-spacing:10px 20px;*/
				/*边框合并  将td的边框和table的边框合并
				合并时会无视table的内边距和td的外边距*/
				border-collapse:collapse;
			}
			td{
				border:1px solid blue;
				padding:1opx
			}
		</style>
	</head>
	<body>
		<table>	
			<tr>
				<td>aaa</td>	
				<td>bbb</td>
				<td>ccc</td>
			</tr>
			<tr>
				<td>ddd</td>	
				<td>eee</td>
				<td>fff</td>
			</tr>
		</table>
	</body>
</html>
```
display属性
```
<!doctype html>
<html>
	<head>
		<meta charset="UTF-8"/>
		<title>显示方式</title>
		<style type="text/css">
			a{
			border:1px;
			width:69px;
			height:77px;
			background:#ccc url("../img/fee_on.png");
			}
		</style>
	</head>
	<body>
		<!-- display：block,比较常用语<a><span> 这两个标签
		因为他们不是块级元素定义display:block，定义width height的相关CSS属性，才会生效-->
		<a href="#" style="display: block">链接1</a>
		<a href="#" style="display:none ">链接2</a>
		<a href="#" style="display: inline">链接3</a>
		<a href="#" >链接4</a>
		<p style="display:inline">红颜，天上空，对对排成行</p>
		<p>红颜，天上空，对对排成行</p>
		
	</body>
</html>
```
