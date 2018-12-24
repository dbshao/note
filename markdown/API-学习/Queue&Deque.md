<small>
##Queue
Collection的子接口
特点：集合元素遵循先进先出的原则
LinkedList双向列表结构，满足queue的特点，所以linkedList是queue的实现类

###boolean offer(Object obj)
相当于 add
###Object peek()
获得队列中的队首元素
仅仅获得队首元素，不会将其移除
### Object poll()
不仅仅获得队首元素，还同时将其移除
如果队列中没有元素，返回null

##Deque
特点：集合元素遵循先进后出的原则
###boolean push((Object obj);
向栈中添加元素

peek、poll 中deque 和 queue 一样 ，但是要注意顺序问题


