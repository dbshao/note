<small>
不是Collections的子接口，是多行两列的二维结构，每一行为一个集合元素，第一列为键（key），第二列为值（value），键唯一，值可以重复，map又称为“键值对”
通过唯一key可以找到对应的value，但通过value，不一定能找到唯一的key

####Map接口实例化
HashMap为最常用的实现类
Map map=new HashMap();

####Object put(Object key,Object value)
给map添加元素，当第一次添加key，value时，key在集合中没有，则返回null，当再次添加key，value时，key在集合中已经存在，而key唯一，此时就是替换value的操作并将原value返回

####Object get（Object key）
查询map集合元素，因为key唯一，所以只能根据key找value

####Object remove(Object key)
删除map集合元素，因为key唯一，所以只能根据key删除元素，并将对应的value值返回

####int size()
获得map集合的元素个数

####void clear(）
清空map集合元素

###Map元素的遍历
######遍历key
1、获得key的set集合
Set keySet=map.keySet();
2、获得keySet的迭代器
ITerator ite=keySet.
3、通过迭代器进行key的遍历
4、通过便利出来的Key找到对应的value

######遍历Value（不常用）
1、获得values 的Collection集合
2、获得values的迭代器
3、通过迭代器进行value的遍历
4、无法获得key

######遍历Entry（key-value）
1、获得Entry（key-value 的Set集合
2、获得Entry的迭代器
3、通过迭代器进行Entry的遍历
4、无法获得key
```
	Map map = new HashMap();
		map.put("数学", 99);
		map.put("语文", 98);
		map.put("英语", 97);
		System.out.println(map);//{语文=98, 英语=98, 数学=98}
		
		/*
		 * 1）、遍历key
		 * 		step1：获得key的Set的集合
		 * 		step2：获得keySet的迭代器
		 * 		step3：通过迭代器，进行key的遍历
		 * 		step4：通过key，找对应的value
		 */
		//step1：获得key的Set的集合
		Set keySet = map.keySet();
		//step2：获得keySet的迭代器
		Iterator keyIte = keySet.iterator();
		//step3：通过迭代器，进行key的遍历
		while(keyIte.hasNext()){
			Object key = keyIte.next();
			//可以根据key找对应value
			Object value = map.get(key);
			System.out.println("key="+key+",value="+value);
		}
		
		System.out.println("****************");
		/*
		 * 2）、遍历value（不常用）
		 * 		step1：获得value的Collection集合
		 * 		step2：获得values集合的迭代器
		 * 		step3：通过迭代器，进行value的遍历
		 * 		
		 * 		实现不了step4：通过value，找对应的key
		 */
		//step1：获得value的Collection集合
		Collection values = map.values();
		//step2：获得values集合的迭代器
		Iterator valueIte = values.iterator();
		//step3：通过迭代器，进行value的遍历
		while(valueIte.hasNext()){
			Object value = valueIte.next();
			System.out.println("value="+value);
		}
		
		System.out.println("****************");
		/*
		 * 3）、遍历Entry(key-value)
		 * 		step1：获得Entry(key-value)的Set的集合
		 * 		step2：获得entrySet的迭代器
		 * 		step3：通过迭代器，进行Entry的遍历
		 * 		step4：通过entry，获得对应key、value
		 */
		//step1：获得Entry(key-value)的Set的集合
		Set entrySet = map.entrySet();
		//step2：获得entrySet的迭代器
		Iterator entryIte = entrySet.iterator();
		//step3：通过迭代器，进行Entry的遍历
		while(entryIte.hasNext()){
			Object obj = entryIte.next();
			if(obj instanceof Map.Entry){//强制转换
				Map.Entry entry = (Map.Entry)obj;
				System.out.println("entry:"+entry);
				
				//step4：通过entry，获得对应key、value
				Object key = entry.getKey();
				Object value = entry.getValue();
				System.out.println("key="+key+",value="+value);
```

######泛型的应用
```
Map<String,Integer> map = 
				new HashMap<String,Integer>();
		map.put("数学", 99);
		map.put("语文", 98);
		map.put("英语", 97);
		System.out.println(map);//{语文=98, 英语=98, 数学=98}
		
		Map<String,Integer> map2 = 
			new LinkedHashMap<String,Integer>();
		map2.put("数学", 99);
		map2.put("语文", 98);
		map2.put("英语", 97);
		System.out.println(map2);//{数学=99, 语文=98, 英语=97}
		
		Map<String,Integer> map3 = 
			new TreeMap<String,Integer>();
		map3.put("Math", 99);
		map3.put("Chinese", 98);
		map3.put("English", 97);
		System.out.println(map3);//{Chinese=98, English=97, Math=99}
```
