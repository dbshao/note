<small>特点1：一旦创建一个字符串类型对象，并给予初始化，则该对象的值不可发生改变。如果该对象被『重新赋值』，则必定是创建了新对象. 
```
String str = "abc";//1个对象abc，且abc对象的值永远不可改变。
		str = "123";//1个新对象123
```  
特点2：相同对象值可以被多个引用指向。jvm对string 做了优化：如果+两边都是 String 类型的字面量，jvm 会在编译之前，将+的结果，直接写入.class 文件当中
```
	String str1 = "abcd";//1个对象
		//str2会重用str1的引用地址。
		String str2 = "abcd";//0个对象
		System.out.println(str1 == str2);//true
		
		String str5 = "ab" + "cd";//2个对象
		System.out.println(str1 == str5);//true

		String str3 = "ab";//0个对象
		String str4 = str3 + "cd";//1个对象
		System.out.println(str1 == str4);//false
```
特点3：常量池（堆中的一块专属区域，用来存放已经存在的字符串对象内容）上述所有对象，都将被存放在常量池中.
string 类型：不可变长字符串类型，其对象一旦被创建，初始化，则无法再被改变
```
String str6 = new String("abcde");//2个对象
		String str7 = new String("abcde");//1个对象
		System.out.println(str6 == str7);//false
		
		String str8 = "abcde";//0个对象
```
string 类型不擅长经常性的修改内容，以下代码会出现内存泄漏异常
```
string str="abc";
for(int i=0;i<100000000;i++){
  str+="abc";
}
```
#####1.string类型的方法length();
用于计算字符串的字符长度,不区分中英文，每个字符一个长度（空格也是）
```
String str="我爱你中国";
int length=str.length();
System.out.println(length);//5

str="I love you";
length=str.length();
System.out.printlin(length);//10
```
#####2.isEmpty() 
很少用，判断字符串对象是否为""空值
只要用 length()=0；就可以代表字符串为空值
```
str = "abc";
		boolean isEmpty = str.isEmpty();
		System.out.println(isEmpty);//false
		
		str = "";
		isEmpty = str.isEmpty();
		System.out.println(isEmpty);//true
```

#####3.indexof()
用于你给我一个字符，我给你一个下标
查询字符串中，子串第一次所在的位置。
```
string str="thing in java"；
//查看 in 子串在原字符串中第一次出现的位置
int firstIndex=str.indexof("in");
System.out.println(firstIndex);//2
```
######int indexof(String substr, int startIndex)
从指定下标开始，查询子串在原字符串中第一次出现的位置
若没有，则返回-1；
######int lastIndexOf(string subStr)
查询字符串在原字符串中最后一次出现的位置

#####4.String toUpperCase()
将字符串中的小写字母转换为大写字母
```
string str="thing in java"；
str2=str.toUpperCase();//重写接收
System.out.println(str2);
```
######String toLowerCase()
将字符串中的大写字母转换为小写字母
>大小写的转换一般用于验证码的检验

###### 5.boolean startsWith(String startStr)
判定是否以指定字符串开头
```
String str="https://www.baidu.com";
boolean isStart=startsWith("http");
System.out.println(isStart)//true
```
######boolean endsWith(String endStr)
判断是否以指定字符串结尾

>一般用于上传文件的检验（文件扩展名）

#####6.String substring(int startIdex[,int endIndex])
指定下标的截取字符串
如果没有 endIndex，则从指定下标截取到末尾
**注意：Java 中所有的截取原则都是前包括后不包括**
```
String str="https://www.baidu.com";
int startIndex=str.indexof("www.baidu.com");//先查询位置
String subStr=str.substring(startIndex);
```

#####7.char chatAt(int index)
返回指定下标位置的字符。
string str="我爱你中国"
char ch=str.charArt(0);
System.out.println(ch);//我

#####8.trim()
去字符串收尾空格
空白：输出站位的空白字符
如空格键， tab 键，回车符……
```
String str="      我     我   我 爱 你           ";
str=str.trim();
System.out.println(str);//我     我   我 爱 你
```
#####9.boolean contains(string subStr)
判断字符串中，是否包含子串
```
str = "thinking in java";
		boolean isContains = str.contains("java");
		System.out.println("字符串中是否包含java子串："+isContains);
```

######10.boolean equals(String otherStr)
此方法并非 String 类的方法，是从 String 的父类 Object 类中重写过来的，用于比较两个字符串的值是否相同
>==与 equals 的区别：
      ==用于比较两个对象是否相同
      基本类型：比较两个变量的值
     引用类型：比较两个对象的地址指向是否相同
     equals 用于比较两个对象是否相同
     基本类型：不用 equals 比较
     引用类型：比较两个对象的值是否相同

```
string str=new String("abcd");
String str1=new String("abcd");
System.out.println（str=str1）;//false
boolean isEquals=str.equals(str1);
System.out.println(isEquals);//true
```
#####11.boolean equalsIgnoreCase(String otherStr)
忽略大小写比较对象
```
String str2 = "THinKing In JaVa";
		String str3 = "thINkINg iN JAva";
		boolean equalsIgnore = 
				str2.equalsIgnoreCase(str3);
		System.out.println("忽略大小写比较对象值："+equalsIgnore)//true
```
######12、valueOf

![valueOf](http://upload-images.jianshu.io/upload_images/66256-581a96828db262f2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
