<small>
Java 中的异常处理机制：
Java中的异常有两大类：
Error：系统错误，往往是 由软件运行的硬件换件遭破坏所导致的，无法通过Java代码来实现修复。如：机房断电，服务器宕机，网络异常……
Exception：代码异常，往往是由于程序设计的瑕疵，导致代码在运行中发生错误，并导致程序最终无法完成功能的实现，甚至导致程序无法运行，分析错误发生的原因，找到有瑕疵的代码，修复bug更新。其中又分为两类
1、CheckedException：
检查时异常（又名编译期异常）直接由Java编程工具IDE（如eclipse）在编译期对代码判断，给出异常提示，这类异常特点：仅仅 提示异常错误，表示对应的地方可能会由于书写不规范导致异常的发生，目的是为了提醒开发者在此处一定要细心编程不要出现书写错误，这类异常都是Exception 如日期操作时：parseException
IO流操作时FileNotFoundException，IOException，数据库操作时，SQLException

2、UncheckedException
非检查异常（又名运行期异常），是RunTimeException的子类，此类异常的存在就是bug，是由于程序员的设计瑕疵，代码逻辑结构问题导致代码在运行中发生的错误异常。
特点：运行时后台报错，代码运行失败。
如：NullPointerException………………
此类异常在程序开发时没有变异错误提示，只有在运行时后台报错，代码运行失败
如何解决：出现bug分析原因找到错误代码块，给予修复，并更新

Java中的异常处理机制主要就是针对CheckedException（编译期期）异常的处理

####异常处理
java中的异常处理机制
1、CheckedException
检查时异常（编译期异常），
此类异常的出现，是提醒程序员，认真仔细的对待代码。
如果不按照规范来书写，可能会导致相关的异常出现。
编译期异常才是java中需要提前处理的。
有两种解决方案：
1）、向外抛
在代码所在的方法上，直接添加throws 异常。
此方案绝对不是最终解决方案，向上抛，要求
方法调用者，接受到异常是需要处理的。
2）、捕获异常，并处理异常。
语法：
```
  try{
   可能发生异常的代码;
  }catch(可能发生的异常类型){
  捕获到异常后，需要执行的后续代码。
  }
```
```
	public static void exceptionTest() throws ParseException{
		SimpleDateFormat sdf = 
				new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
		
	
		Date date = 
				sdf.parse("2016-1020 14:06:00");
	}

	public static void main(String[] args) {
		/*

		try{
			//可能发生异常的代码;
			exceptionTest();
		}catch(ParseException e /*可能发生的异常类型*/){
			
			//打印异常的堆栈信息，为了方便异常的修复。
			e.printStackTrace();
			
			//捕获到异常后，需要执行的后续代码。
			System.out.println("捕获到了ParseException异常。");
```

try-catch-finally 还可以做以下操作：
2）、捕获异常，并处理异常。
```
 * 			try - catch - finally
 * 
 * 			语法：
 * 			try{
 * 				可能发生异常的代码;
 * 			}catch(可能发生的异常类型1){
 * 				捕获到异常后，需要执行的后续代码。
 * 			}
 * 			......//catch多个
 * 			finally{
 * 				最终需要执行的代码
 * 				//最终：无论是否捕获异常。
 * 			}
 * 
 * 			注意：
 * 				a、try、finally只能一次，catch可以没有。
 * 				b、finally可以直接跟在try后。
 * 
 * 	Java异常处理机制的解决之道：
 * 		****能捕获就捕获，捕获不了再向外抛。
```
#####java中的异常处理机制
throw、throws关键字
1）、throw
认为的就地抛出一个异常。
用在代码中。
2）、throws
方法可能会抛出某类异常。
至于最后会不会抛出异常，看代码。
用在方法上。
```
public static void throwTest(){
		System.out.println("throwTest");
		//就地抛出一个空指针异常。
		throw new NullPointerException();
	}
	public static void throwsTest()
				throws NullPointerException{
		System.out.println("throwsTest");
	}
	
	public static void main(String[] args) {
//		throwTest();
		
		throwsTest();
	}
```
> #####finalize、final、finally关键字
 * 		
 * 		1）、finalize
 * 			Object类中的方法
 * 			用于判断堆中是否含有没有引用指向的对象内存。
 * 			在GC方法前执行。
 * 		
 * 		2）、final
 * 			修饰符
 * 			修饰的变量是常量，一旦初始化，就不能改变其值。
 * 			修饰的方法，无法被重写。
 * 			修饰的类，无法被继承。
 * 
 * 		3）、finally
 * 			Java中异常处理机制中的关键字。
 * 			try - catch - finally
 * 			finally中执行的代码块，无论是否发生异常，
 * 			都将会被执行的代码。

```
finally里面，绝对不建议使用return关键字。
 * 		因为finally中使用return，
 * 		可能会影响到代码的真实结果。
```
例子如下：
```
public static void main(String[] args) {
		System.out.println(test(null));//3
		System.out.println(test("a"));//3
		System.out.println(test("我爱你中国！"));//3
	}
	public static int test(String str){
		try{
			str.toString();
			str.charAt(5);
			return 0;
		}catch(NullPointerException e){
			return 1;
		}catch(StringIndexOutOfBoundsException e){
			return 2;
		}finally{
//			return 3;
```

#####自定义异常
步骤：step1：自定义异常类继承Exception
step2：定义异常构造
自定义异常就是CheckedException。
```
public class ExceptionDemo07 {
	public static void main(String[] args) {
		//模拟卡内余额不足，调用自定义异常
		Scanner sc = new Scanner(System.in);
		double money = sc.nextDouble();
		if(money > 100){
			//模拟卡中只有100
			try {
				throw new NoMoreMoneyException();
			} catch (NoMoreMoneyException e) {
				e.printStackTrace();
			}
		}else if(money > 0){
			System.out.println("请取走你的现金...");
		}else{
			try {
				throw new NoMoreMoneyException("输入金额非法");
			} catch (NoMoreMoneyException e) {
				e.printStackTrace();
			}
		}
	}
}

//step1：自定义异常类继承Exception
class NoMoreMoneyException extends Exception{
	public NoMoreMoneyException() {
		System.out.println("卡内余额不足");
	}

	public NoMoreMoneyException(String arg0, Throwable arg1, boolean arg2,
			boolean arg3) {
		super(arg0, arg1, arg2, arg3);
		// TODO Auto-generated constructor stub
	}

	public NoMoreMoneyException(String arg0, Throwable arg1) {
		super(arg0, arg1);
	}

	public NoMoreMoneyException(String arg0) {
		super(arg0);
	}

	public NoMoreMoneyException(Throwable arg0) {
		super(arg0);
		// TODO Auto-generated constructor stub
	}
}
```
######Exception方法介绍
```
public static void main(String[] args) throws FileNotFoundException {
		Exception e = new NullPointerException();
		/*
		 * 1、打印异常堆栈信息
		 */
//		e.printStackTrace();
		
		/*
		 * 2、异常信息
		 */
//		System.out.println(e.getMessage());
		
		/*
		 * 3、异常的发生原因
		 */
		System.out.println(e.getCause());
		
		/*
		 * 4、将异常的堆栈信息，记录在指定文件中。
		 * 		对应的文件，被称为错误信息日志。
		 * 		便于日后的BUG修复、维护。
		 */
		PrintWriter pw = new PrintWriter("error.txt");
		e.printStackTrace(pw);
```
