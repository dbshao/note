<small>
#####1.StringBuilder 类
可变长字符串类型，经常修改 String 类型的引用值，建议使用这个
```
string→StringBulider
StringBulider sb=new StringBuilder( );//创建空字符串不是 null
String str1="我爱你中国"
StringBulider sb=new StringBuilder( str1);
String str2=sb.toString;
```
######增 append(String subStr)
确实可以返回一个StringBulider，但是并不需要,StringBulider自身维护一个可变长度的字符序列，每当调用 append 方法时，就会根据 append 子串长度，对自身维护字符序列进行相应的扩容，然后将子串字符序列，依次写入扩容后的 String
所以只要经过 append 方法，StringBulider原序列就已经发生了变化
```
StringBulider sb=new StringBulider("学号 java")；
sb=sb.append(",走遍天下都不怕")；//不好的写法
sb.append(",走遍天下都不怕"）；//正确的写法
System.out.println(sb);//学好 Java，走遍天下都不怕
```
######删delete(int startIndex，int endIndex)
也是前包括后不包括原则
```
sb.delete(7,15);//学号 Java,
sb.append("为了更好地工作"）//学好 java,为了更好的工作！
```
######改replace(int start,int end,String Str)
```
sb.replace(7,14,"为了改变世界");//学好 java，为了改变世界
```
######插insert(int insertIndex, String subString)
在指定下标前，插入子串
```
sb.insert(7,"努力工作，");//学好 java，努力工作，为了改变世界！
```

2.StringBuffer :可变长字符串类型
与StringBulider一样都有增删改插等方法
两者区别与联系：
1、两者在物理方法上，完全一模一样
2、StringBuffer 是线程安全的，性能慢
StringBulider是线程不安全的，性能快

>如今服务器性能已近得到很大程度的提升，如果在可以忽略两者的微弱的性能差异，两者随便使用
但是需要考虑到两者的线程安全问题

String Buffer 中含有 reverse 方法可以将字符串逆转；
