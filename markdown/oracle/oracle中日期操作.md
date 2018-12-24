##日期类型
Date：oracle中常用的日期类型，保存日期和时间，固定七个字节，第一个字节；世纪+100，第二到第七是年月日时分秒，其中时分秒+1
日期关键字：sysdate，返回当前系统时间，精确到秒，默认 格式：dd-mm月-yy
Timestamp：oracle中常用的日期类型保存日期和时间，还能保存小数的秒，最高精确到ns，前七个字节与date一致，后四个字节用来储存内部运算的精确值。
日期关键字：systimestamp，返回当前系统时间，精确到毫秒
##日期函数
#####1、日期转换为字符串
to_char(date,fromat) \
将date类型的日期，以format置顶的格式，转换成字符串时间
这里的格式与Java不一样（由于oracle不区分大小写）
Java中 yyyy-MM-dd HH:mm:ss 
oracle中 yyyy-MM-dd HH24:mi:ss 
对于中文字符需要原样输入则需要添加双引号
如： yyyy“年”MM“月”dd“日” HH24“时”mi“分”ss “秒”
#####2、字符串转换成日期
to_date（dateStr，format）
select to_date（'dateStr'，yyyy-MM-dd HH24:mi:ss ）from dual;
> 对很长的字符段可以进行取别名 在查询的后面加上 别名或者 用as 别名
中文也可以直接输入不需要加引号


#####3、两个日期直接相减
date1-date2
得到的天数有小数点，可以精确
moths_between（date1,date2）
两个日期的月数之差，有小数点
日期和数字直接加减，都是表示日期加减天数
add_months(date,month）
返回date日期加上moths个月后的日期
>如果month为负数表示减，如果month是小数，则忽略小数，直接截除

####4、last_day（date）
指定日期所在月的最后一天
#####5、next_day（date,char）
指定日期对应的下一个周几
注意：不是下一天，也不是下周几，是下一个周几，这里的周几用1~7代替周末是1


######6、日期比较
least（date1,date2……）
返回日期比较后的最小日期
greatest（date1，date2……）
返回日期比较后的最大日期
比较规则：在比较之前，以第一个参数类型为准，在参数列表中，将第二个及其以后的参数自动默认隐含的转换成第一个参数类型，如果能转，继续比较，如果转不了，报错
least、greatest不仅仅能比较日期，还可以比较其他类型，如字符串，数值等

#####7、从日期中提取日期分量
extract（datePart from date）
日期分量：年月日  时分秒
年月日 sysdate 有，时分秒 sysdate没有，systimestamp
注意查询的时间要加上当前时区

#####任意时间的操作
date+interval'整数'单位
select systimestamp +interval ‘10’ minutes from dual
