<small>
##1、促销日代码
用户输入商品生产日期和保质期，通过程序计算促销日期。计算规则为：到保质期前14天所在周的周三为促销日。控制台交互情况如图-1所示。



![图1](http://upload-images.jianshu.io/upload_images/66256-e1bd65f55fd3f87d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


```
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Date;
import java.util.Scanner;

public class Deline {
	public static  void main(String[] args) throws ParseException{
		Calendar cal=Calendar.getInstance();
		System.out.println("请输入生产日期（yyyy-MM-dd）：");
		Scanner sc=new Scanner(System.in);
		String str= sc.nextLine();
		System.out.println("请输入保质期：");
		int day=sc.nextInt();
		SimpleDateFormat sdf=new SimpleDateFormat("yyyy-MM-dd");
		Date bothDate=sdf.parse(str);
		cal.setTime(bothDate);
		cal.add(Calendar.DATE,day-14);
		cal.set(Calendar.DAY_OF_WEEK,Calendar.WEDNESDAY);
		System.out.println("促销日为："+sdf.format(cal.getTime()));
	}

}
```
