<small>
###List集合
collection接口下的子接口
集合特点：元素添加与输出有序，元素可重复
List接口无法实例化
**可以通过下标操作元素（List最大特点）**

List list=new ArrayList（）；
list.add("java")
list.add("C")
list.add("java")
list.add("php")
system.out.println(list);

#####add (int index.Object obi)
list.add(2,"IOS")
指定下标的添加集合元素，原位置元素依次向后移位
插入元素

###Object(E) remove（int index）
制定下标移除元素，并将移除元素返回
Object obj=list.remove(3);

###set(int index,Object obj)
指定下标的元素替换，并返回替换的元素
Object obj1=list.set(list.size()-1,".NET")

###object get(int index)
类似于数组Array（index）
Object obj2=list.get(4);

###int indexOf(Object obj)
获得指定元素的下标位置
int cIndex=list.indexOf("C");

###addAll(int index, List list)
指定下标的添加整体

###boolean euqals(Collection col)
比较两个集合值是否相同
注意：顺序比较，元素顺序要一致

由于List集合可以通过下标操作元素的特点，所以可以通过普通的for循环来实现集合遍历
```
//方式一：普通for循环
		for(int i=0; i<list.size(); i++){
			System.out.println(list.get(i));
		}
		System.out.println("***********************");
		//方式二：迭代器
		Iterator ite = list.iterator();
		while(ite.hasNext()){
			System.out.println(ite.next());
		}
		System.out.println("***********************");
		//方式三：增强for循环
		for(Object obj : list){
			System.out.println(obj);
```


###List sublist=list.sublist(2,8)
截取集合,截取后返回一个子集合
注意事项：返回的子集合并非是新对象，而是直接将元对象中的元素给予繁育呈现出来而已，若想改变子集合的元素内容，则必定会导致原集合元素也发生改变，
建议：不要对子集合进行元素修改操作
List list=new ArrayList（）；


###object[] toArray()
集合→数组
将集合转换为Object类型的数组
将集合转换为指定类型的数组时，要对集合指定泛型
Object[] objs=List.toArray();
String[] str=list.
集合转换过来的数组是一个新对象，对数组的元素使用不会影响到原集合
###数组→集合
通过Arrays工具类中的asList方法
List<T> asList(T list)
List list=Arrays.asList(strs);
数组转换过来的集合不是新对象，而是对数组的另一种呈现方式，对集合元素操作，其本质就是对数组元素的操作。
集合不允许做增删操作（不能改变元素个数），只可以实现元素内容的替换操作，集合元素的改变，必定会影响到原数组
```
List<String> list = new ArrayList();
		list.add("java");
		list.add("C");
		list.add(".NET");
		list.add("PHP");
		System.out.println("list集合："+list);
		
		/*
		 * 集合 → 数组
		 * 1、方法1：集合转换成Object类型的数组
		 * 		Object[] toArray()
		 * 
		 * 2、方法2：集合转换成指定类型的数组
		 * 		T[] toArray(T[] t)
		 * 		注意：必须要求集合有泛型指定。
		 */
		Object[] objs = list.toArray();
		System.out.println("list转换成数组："+ Arrays.toString(objs));
		
		String[] strs = list.toArray(new String[list.size()]);
		System.out.println("list转换成指定泛型的数组："+ Arrays.toString(strs));
		
		/*
		 * 集合转换过来的数组，特点：
		 * 	 1、集合转换过来的数组是一个新对象，
		 * 		对数组元素使用不会影响到原集合。
		 */
		strs = Arrays.copyOf(strs, strs.length+1);
		strs[strs.length-1] = "我爱你";
		System.out.println("扩容之后的数组："+ Arrays.toString(strs));
		
		System.out.println("数组扩容后的集合："+list);
```

**集合的底层实现，其实就是数组**



![转换](http://upload-images.jianshu.io/upload_images/66256-6c6dcf230e8865a5.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##List总结：
1、集合特点：添加有序，可重复，可通过下标操作元素
2、实现类：ArrayList，LinkedList，Vector
物理方法上，三者阿迷区别，性能上有所区别
ArrayList：线性结构，查询快，增删慢
LinkedList：双向链表结构，查询慢，增删快
Vector：ArrayList与LinkedList都是非线程安全的，vector是线程安全的

##set集合总结：
也是Collections的子接口
特点：添加与输出顺序不一致，简称添加无序
  元素补课重复
如果要想添加与输出的顺序一致
可以使用Set的子接口的LinkedHashSet
Set set=new HashSet();
如果想让Set集合元素实现自然排序，可以用TreeSet
