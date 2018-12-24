<small>
  

public class **Object**
类 Object 是类层次结构的根类。每个类都使用 Object 作为超类。所有对象（包括数组）都实现这个类的方法。
#####1、equals()
相等于==

Object 类的 equals 方法实现对象上差别可能性最大的相等关系；即，对于任何非空引用值 x 和 y，当且仅当 x 和 y 引用同一个对象时，此方法才返回 true（x == y 具有值 true）。
注意：当此方法被重写时，通常有必要重写 hashCode 方法，以维护 hashCode 方法的常规协定，该协定声明相等对象必须具有相等的哈希码。

#####2、toString()
返回该对象的字符串表示
Object 类中的 toString 是类名@16进制的 哈希值
//如何直观的看到该对象的属性？重写方法
```
public String toString(){
//标准型
return this.getClass().getName()+
//简单型
"@["name=this.name"+age=this.age]
}
```
```
String str="123456";
System.out.println(str.toString);//123456
pe0.toString;//类名@哈希值

```
>注意：Object中的 euqals 和 toString 与 String 中的euqals 和 toString 是不同的，String 类已经将这两个方法进行了重写

toString 和 equals 方法的重写可以参照如下：
```
	/*
	 * 为了能够更加直观的打印出对象的内容。
	 * 	则必须重写Object中的toString方法
	 */
	@Override
	public String toString(){
		//标准型
		return //this.getClass().getName()+
				//"@" +
		//简易型
				"[" +
					"name="+this.name+"," +
					"age="+this.age+
				"]";
	}
	
	/**
	 *  从值面量上，可以看出，peo于peo1是相等的。
		但是Object的equals方法满足不了，所以我们需要重写。
		
		equals方法判断的是两个对象内容。
	 * @return
	 */
	@Override
	public boolean equals(Object other){
		if(other == null){//判空
			return false;
		}
		if(other == this){//同一个对象
			return true;
		}
		if(other instanceof People){//类型匹配
			//同类型对象才可比。
			People otherPeo = (People)other;
			//如果名字相同、年龄相同，才说明两个对象值相同
			return this.name.equals(otherPeo.name)
					&&
					this.age == otherPeo.age;
		}
		return false;
	}
```
