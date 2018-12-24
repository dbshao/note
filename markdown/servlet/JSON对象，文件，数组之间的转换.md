

![js中的转换](http://upload-images.jianshu.io/upload_images/66256-f777e621ba22d4d9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
		function f1(){
				var str='{"name":"hanmeime","age":17}';
				//第一种方式:eval函数
				//var obj=eval("("+str+")");
				//第二种：使用JSON对象
				//var obj=JSON.parse(str);
				//第三种：需要josn.js文件
				var arr=str.parseJSON();
				alert(obj.name);
			}
			
			//JSON字符串转JSON数组
			function f2(){
				var str='[{"name":"hanmeime","age":17},' +
				            '{"name":"lilei","age":17}]';
				//1.使用eval
				//var arr=eval("("+str+")");
				//2
				var arr=JSON.parse(str);
				alert(arr[1].name);
			}
			
			//JSON对象转JSON字符串
			function f3(){
				var obj={"name":"hanmeime","age":17};
				//1.要引入json.js
				//var str=obj.toJSONString();
				//2.
				var str=JSON.stringify(obj);
				alert(str);
			}
```


![servlet中的转换](http://upload-images.jianshu.io/upload_images/66256-e02b66234ec0ee5c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
	public static void test1(){
		Friend f=new Friend();
		f.setName("lilei");
		f.setAge(17);
		JSONObject jsonObj=JSONObject.fromObject(f);
		String jsonStr=jsonObj.toString();
		System.out.println(jsonStr);
	}
	/*
	 * java数组/集合转JSON字符串
	 */
	public static void test2(){
		List<Friend> fs=new ArrayList<Friend>();
		for(int i=0;i<3;i++){
			Friend f=new Friend();
			f.setName("jack"+i);
			f.setAge(19+i);
			fs.add(f);
		}
		JSONArray jsonArr=JSONArray.fromObject(fs);
		String jsonStr=jsonArr.toString();
		System.out.println(jsonStr);
	}
	
	/*
	 * JSON字符串转成java对象
	 */
	
	public static void test3(){
		String jsonStr="{\"name\":\"liming\",\"age\":17}";
		JSONObject jsonObj=JSONObject.fromObject(jsonStr);
		Friend friend=(Friend)JSONObject.toBean(jsonObj,Friend.class);
		System.out.println(friend);
	}
	
	/*
	 * JSON字符串转成java数组
	 */
	public static void test4(){
		String jsonStr="[{\"name\":\"liming\",\"age\":17}," +
				        "{\"name\":\"lilei\",\"age\":19}]";
		JSONArray jsonArr=JSONArray.fromObject(jsonStr);
		List<Friend> friends=
			(List<Friend>)JSONArray.toCollection(jsonArr,Friend.class);
		for(Friend f: friends){
			System.out.println(f);
		}
	}
```
