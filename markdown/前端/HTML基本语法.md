常见代码以及显示效果
```
<!Doctype html>
<html>
<head>
<meta charset="UTF-8"/>
<title>文本</title>
<body>
		<p><b>北京市</b><i>海定区</i>北三环西平路<del>18号</del><span style="color:red">中鼎大厦</span><u>B座&lt7层&gt</u></P>
		
		<!-- 空格折叠，HTML中文字间多个空格或者换行，以及缩进，都当做一个空格对待 -->
		那是一个秋天 
		看着老程跑偏
		 奔着娇娇而去 
		 误入老王心间
		<p>
		那   是一个秋天 <br/>
		看着老程跑偏<br/>
		 奔着娇娇而去 <br/>
		 误入老王心间<br/>
		</p>
		
		<!-- 标题 -->
		<h1>程程</h1>
		<h1>娇娇</h1>
		<h3>老王</h3>
		
		<!-- 段落P 可以默认限制大小，还能独立成行，直接写文字并换行是不会独立成行的 -->
		<p>程程找娇娇，娇娇不在</p>
		<div>
		<p>段落一 </p>
		<p>段落二</p>
		<ol>1<ol>
		</div>
		
		<!-- 图片的访问 -->
		<!-- 绝对路径 -->
		<img  src="E:/图片1.png"/>
		<!-- 相对路径    ../表示向上跳一级-->
		<img  src="../images/1.jpg"/>
</body>
</head>
</html>
```


![效果展示](http://upload-images.jianshu.io/upload_images/66256-4ef2452f7152c47f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
