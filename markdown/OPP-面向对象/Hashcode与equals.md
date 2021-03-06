1. 首先equals()和hashcode()这两个方法都是从object类中继承过来的。
``` 
equals()方法在object类中定义如下： 
  public boolean equals(Object obj) { 
return (this == obj); 
} 
```
很明显是对两个对象的地址值进行的比较（即比较引用是否相同）。但是我们必需清楚，当String 、Math、还有Integer、Double。。。。等这些封装类在使用equals()方法时，已经覆盖了object类的equals（）方法。
```
比如在String类中如下： 
  public boolean equals(Object anObject) { 
if (this == anObject) { 
    return true; 
} 
if (anObject instanceof String) { 
    String anotherString = (String)anObject; 
    int n = count; 
    if (n == anotherString.count) { 
char v1[] = value; 
char v2[] = anotherString.value; 
int i = offset; 
int j = anotherString.offset; 
while (n-- != 0) { 
    if (v1[i++] != v2[j++]) 
return false; 
} 
return true; 
    } 
} 
return false; 
} 
```
很明显，这是进行的内容比较，而已经不再是地址的比较。依次类推Double、Integer、Math。。。。等等这些类都是重写了equals()方法的，从而进行的是内容的比较。当然了基本类型是进行值的比较，这个没有什么好说的。 
我们还应该注意，Java语言对equals()的要求如下，这些要求是必须遵循的： 
• 对称性：如果x.equals(y)返回是“true”，那么y.equals(x)也应该返回是“true”。 
• 反射性：x.equals(x)必须返回是“true”。 
• 类推性：如果x.equals(y)返回是“true”，而且y.equals(z)返回是“true”，那么z.equals(x)也应该返回是“true”。 
• 还有一致性：如果x.equals(y)返回是“true”，只要x和y内容一直不变，不管你重复x.equals(y)多少次，返回都是“true”。 
• 任何情况下，x.equals(null)，永远返回是“false”；x.equals(和x不同类型的对象)永远返回是“false”。 
以上这五点是重写equals()方法时，必须遵守的准则，如果违反会出现意想不到的结果，请大家一定要遵守。 

2. 其次是hashcode() 方法，在object类中定义如下： 
  public native int hashCode(); 
说明是一个本地方法，它的实现是根据本地机器相关的。当然我们可以在自己写的类中覆盖hashcode()方法，比如String、Integer、Double。。。。等等这些类都是覆盖了hashcode()方法的。
```
例如在String类中定义的hashcode()方法如下： 
    public int hashCode() { 
int h = hash; 
if (h == 0) { 
    int off = offset; 
    char val[] = value; 
    int len = count; 

            for (int i = 0; i < len; i++) { 
                h = 31*h + val[off++]; 
            } 
            hash = h; 
        } 
        return h; 
} 
```
解释一下这个程序（String的API中写到）： 
s[0]*31^(n-1) + s[1]*31^(n-2) + ... + s[n-1] 
使用 int 算法，这里 s[i] 是字符串的第 i 个字符，n 是字符串的长度，^ 表示求幂。（空字符串的哈希码为 0。） 

3.这里我们首先要明白一个问题： 
equals()相等的两个对象，hashcode()一定相等； 
equals（）不相等的两个对象，却并不能证明他们的hashcode()不相等。换句话说，equals()方法不相等的两个对象，hashcode()有可能相等。（我的理解是由于哈希码在生成的时候产生冲突造成的）。 
反过来：hashcode()不等，一定能推出equals()也不等；hashcode()相等，equals()可能相等，也可能不等。解释下第3点的使用范围，我的理解是在object、String等类中都能使用。在object类中，hashcode()方法是本地方法，返回的是对象的地址值，而object类中的equals()方法比较的也是两个对象的地址值，如果equals()相等，说明两个对象地址值也相等，当然hashcode()也就相等了；在String类中，equals()返回的是两个对象内容的比较，当两个对象内容相等时， 
Hashcode()方法根据String类的重写（第2点里面已经分析了）代码的分析，也可知道hashcode()返回结果也会相等。以此类推，可以知道Integer、Double等封装类中经过重写的equals()和hashcode()方法也同样适合于这个原则。当然没有经过重写的类，在继承了object类的equals()和hashcode()方法后，也会遵守这个原则。 

4.谈到hashcode()和equals()就不能不说到hashset,hashmap,hashtable中的使用，具体是怎样呢，请看如下分析： 
Hashset是继承Set接口，Set接口又实现Collection接口，这是层次关系。那么hashset是根据什么原理来存取对象的呢？ 
在hashset中不允许出现重复对象，元素的位置也是不确定的。在hashset中又是怎样判定元素是否重复的呢？这就是问题的关键所在，经过一下午的查询求证终于获得了一点启示，和大家分享一下，在java的集合中，判断两个对象是否相等的规则是： 
1)，判断两个对象的hashCode是否相等 
      如果不相等，认为两个对象也不相等，完毕 
      如果相等，转入2) 
（这一点只是为了提高存储效率而要求的，其实理论上没有也可以，但如果没有，实际使用时效率会大大降低，所以我们这里将其做为必需的。后面会重点讲到这个问题。） 
2)，判断两个对象用equals运算是否相等 
      如果不相等，认为两个对象也不相等 
      如果相等，认为两个对象相等（equals()是判断两个对象是否相等的关键） 
为什么是两条准则，难道用第一条不行吗？不行，因为前面已经说了，hashcode()相等时，equals()方法也可能不等，所以必须用第2条准则进行限制，才能保证加入的为非重复元素。 
比如下面的代码： 
```
public static void main(String args[]){ 
String s1=new String("zhaoxudong"); 
String s2=new String("zhaoxudong"); 
System.out.println(s1==s2);//false 
System.out.println(s1.equals(s2));//true 
System.out.println(s1.hashCode());//s1.hashcode()等于s2.hashcode() 
System.out.println(s2.hashCode()); 
Set hashset=new HashSet(); 
hashset.add(s1); 
hashset.add(s2); 
/*实质上在添加s1,s2时，运用上面说到的两点准则，可以知道
hashset认为s1和s2是相等的，是在添加重复元素，所以让s2覆盖了s1;*/ 
Iterator it=hashset.iterator(); 
            while(it.hasNext()) 
            { 
             System.out.println(it.next()); 
            } 
```
最后在while循环的时候只打印出了一个”zhaoxudong”。 
输出结果为：false 
            true 
            -967303459 
            -967303459 
这是因为String类已经重写了equals()方法和hashcode()方法，所以在根据上面的第1.2条原则判定时，hashset认为它们是相等的对象，进行了重复添加。 
但是看下面的程序：
``` 
import java.util.*; 
public class HashSetTest 
{ 
   public static void main(String[] args) 
    { 
                 HashSet hs=new HashSet(); 
                 hs.add(new Student(1,"zhangsan")); 
                 hs.add(new Student(2,"lisi")); 
                 hs.add(new Student(3,"wangwu")); 
                 hs.add(new Student(1,"zhangsan")); 
  
                 Iterator it=hs.iterator(); 
                 while(it.hasNext()) 
                 { 
                        System.out.println(it.next()); 
                 } 
     } 
} 
class Student 
   { 
     int num; 
     String name; 
     Student(int num,String name) 
                { 
                this.num=num; 
                 this.name=name; 
                 } 
              public String toString() 
                { 
                    return num+":"+name; 
                 } 
           }      
输出结果为： 
                      1:zhangsan 
                   1:zhangsan 
                   3:wangwu 
                   2:lisi 
```
问题出现了，为什么hashset添加了相等的元素呢，这是不是和hashset的原则违背了呢？回答是：没有 
因为在根据hashcode()对两次建立的new Student(1,"zhangsan")对象进行比较时，生成的是不同的哈希码值，所以hashset把他当作不同的对象对待了，当然此时的equals()方法返回的值也不等（这个不用解释了吧）。那么为什么会生成不同的哈希码值呢？上面我们在比较s1和s2的时候不是生成了同样的哈希码吗？原因就在于我们自己写的Student类并没有重新自己的hashcode()和equals()方法，所以在比较时，是继承的object类中的hashcode()方法，呵呵，各位还记得object类中的hashcode()方法比较的是什么吧！！ 
它是一个本地方法，比较的是对象的地址（引用地址），使用new方法创建对象，两次生成的当然是不同的对象了（这个大家都能理解吧。。。），造成的结果就是两个对象的hashcode()返回的值不一样。所以根据第一个准则，hashset会把它们当作不同的对象对待，自然也用不着第二个准则进行判定了。那么怎么解决这个问题呢？？ 
答案是：在Student类中重新hashcode()和equals()方法。 
```
例如： 
  class Student 
{ 
int num; 
String name; 
Student(int num,String name) 
{ 
            this.num=num; 
            this.name=name; 
} 
public int hashCode() 
{ 
            return num*name.hashCode(); 
} 
public boolean equals(Object o) 
{ 
            Student s=(Student)o; 
            return num==s.num && name.equals(s.name); 
} 
public String toString() 
{ 
            return num+":"+name; 
} 
} 
```
根据重写的方法，即便两次调用了new Student(1,"zhangsan")，我们在获得对象的哈希码时，根据重写的方法hashcode()，获得的哈希码肯定是一样的（这一点应该没有疑问吧）。 
当然根据equals()方法我们也可判断是相同的。所以在向hashset集合中添加时把它们当作重复元素看待了。所以运行修改后的程序时，我们会发现运行结果是： 
                      1:zhangsan 
                   3:wangwu 
                   2:lisi 
可以看到重复元素的问题已经消除。 
关于在hibernate的pojo类中，重新equals()和hashcode()的问题： 
1)，重点是equals，重写hashCode只是技术要求（为了提高效率） 
2)，为什么要重写equals呢，因为在java的集合框架中，是通过equals来判断两个对象是否相等的 
3)，在hibernate中，经常使用set集合来保存相关对象，而set集合是不允许重复的。我们再来谈谈前面提到在向hashset集合中添加元素时,怎样判断对象是否相同的准则，前面说了两条，其实只要重写equals()这一条也可以。 
但当hashset中元素比较多时，或者是重写的equals()方法比较复杂时，我们只用equals()方法进行比较判断，效率也会非常低，所以引入了hashcode()这个方法，只是为了提高效率，但是我觉得这是非常有必要的（所以我们在前面以两条准则来进行hashset的元素是否重复的判断）。 
>比如可以这样写： 
public int hashCode(){ 
   return  1;}//等价于hashcode无效 
这样做的效果就是在比较哈希码的时候不能进行判断，因为每个对象返回的哈希码都是1，每次都必须要经过比较equals()方法后才能进行判断是否重复，这当然会引起效率的大大降低。 
我有一个问题，如果像前面提到的在hashset中判断元素是否重复的必要方法是equals()方法（根据网上找到的观点），但是这里并没有涉及到关于哈希表的问题，可是这个集合却叫hashset，这是为什么？？ 
我想，在hashmap,hashtable中的存储操作，依然遵守上面的准则。所以这里不再多说。这些是今天看书，网上查询资料，自己总结出来的，部分代码和语言是引述，但是千真万确是自己总结出来的。有错误之处和不详细不清楚的地方还请大家指出，我也是初学者，所以难免会有错误的地方，希望大家共同讨论。
