<small>
###猜字母游戏
为猜字母游戏添加游戏等级。游戏等级设为三等：5、7和9，代表所需要猜测的字母个数。游戏开始时，由玩家选择游戏等级（5，7，9）。如果选择7，则会随机产生7个字符，然后玩家输入一个字符串包含7个字符，看这7个字符和随机产生的7个字符比较，看是否正确，并统计分数。另外，如果输入其它，重新提示输入游戏等级。系统交互情况如图所示：

![图](http://upload-images.jianshu.io/upload_images/66256-14b02fecde26c048.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```
package homework;

import java.util.Arrays;
import java.util.Random;
import java.util.Scanner;

public class GussLetters {

	/**为猜字母游戏添加游戏等级。
	 * 游戏等级设为三等：5、7和9，
	 * 代表所需要猜测的字母个数。游戏开始时，
	 * 由玩家选择游戏等级（5，7，9）。
	 * 如 果选择7，则会随机产生7个字符，
	 * 然后玩家输入一个字符串包含7个字符，
	 * 看这7个字符和随机产生的7个字符比较，
	 * 看是否正确，并统计分数。另外，如果输入 其它，
	 * 重新提示输入游戏等级。
	 * @param args
	 */
	public static void main(String[] args) {
		System.out.println("GussingGame>>欢迎尝试猜字母游戏！");
		Scanner sc = new Scanner(System.in);
		//输入游戏等级
		int level = getLevel(sc);
		
		//随机产生level个字符
		char[] randomChars = getRandomChars(level);
		
		//游戏开始
		gameStart(sc, level, randomChars);
	}

	/**
	 * 猜字母游戏
	 * 		控制台输入对应级别的字符序列
	 * 		与随机产生的字符序列进行对比。
	 *		并将最后的对比结果进行打印。
	 * @param sc 控制台扫描器，用于进行控制台猜字母扫描
	 * @param level 对应的游戏级别
	 * @param randomChars 随机产生的字符序列数组
	 */
	private static void gameStart(Scanner sc, int level, char[] randomChars) {
		//游戏开始 
		//控制台输入所要猜的字母序列 start
		char[] gusseingChars = new char[level];
		//记录总次数
		int totalGusseCount = 0;
		System.out.println("GussingGame>>游戏开始，请输入您所猜的"+level+"个字母的序列：(exit-退出)");
		while(true){
			//输入字符串
			String gusseingStr = sc.next();
			//输入的是exit，则退出游戏
			if("exit".equals(gusseingStr)){
				break;
			}
			//如果输入的字符串长度不等于level，输入无效，重新输入。
			if(gusseingStr.length() != level){
				System.out.println("GussingGame>>您的输入字符个数有误，请重新输入：(exit-退出)");
				continue;
			}
			//将字符串转成大写，再转换换成字符数组
			gusseingChars = 
				gusseingStr.toUpperCase().toCharArray();
			
			//随机字符数组、人工猜测字符数组对比
			int[] rights = 
				checkChars(randomChars,gusseingChars);
			
			//结果打印：																							      //猜一次 加一次。
			System.out.println("GussingGame>>您猜对了"+rights[0]+"个字符，其中"+rights[1]+"个字符的位置正确！（总次数是"+(++totalGusseCount)+",exit-退出）");
			
			//都猜对了，自动结束
			if(rights[1] == level){
				break;
			}
			
		}
		//控制台输入所要猜的字母序列 end
	}

	/**
	 * 产生随机字符序列
	 * @param level 游戏级别
	 * @return 随机字符序列数组
	 */
	private static char[] getRandomChars(int level) {
		//随机产生level个字符 start
		//随机字符数组
		char[] randomChars = new char[level];
		char[] chars = {'A','B','C','D','E','F','G',
						'H','I','J','K','L','M','N',
						'O','P','Q','R','S','T',
						'U','V','W','X','Y','Z'}; 
		boolean[] randomIndexs = new boolean[chars.length];
		//随机数
		Random ran = new Random();
		for(int i=0; i<randomChars.length; i++){
			int index = ran.nextInt(26);//[0,26)即[0,25]其中的整数
			//判断该下标对应的字母是否已被取出
			if(randomIndexs[index]){
				//已经取出，本次随机无效，继续本次随机。
				i--;
				continue;
			}
			//本次随机有效，取出子字母，并将对应开关开启。
			randomChars[i] = chars[index];
			randomIndexs[index] = true;
		}
		System.out.println(Arrays.toString(randomChars));
		//随机产生level个字符 end
		return randomChars;
	}

	/**
	 * 获得游戏级别
	 * @param sc 控制台扫描器，扫描输入的游戏级别
	 * @return 游戏级别
	 */
	private static int getLevel(Scanner sc) {
		int level = 0;
		//输入游戏级别
		while(true){
			System.out.print("GussingGame>>请输入游戏级别（5、7、9）？");
			level = sc.nextInt();
			//如果输入的是5、7、9，则退出循环。
			if(level==5 || level==7 || level==9){
				break;
			}
		}
		return level;
	}
	
	/**
	 * 随机字符序列数组、控制台人工猜测字符序列数组
	 * 	对比方法
	 * @param randomChars 随机字符序列数组
	 * @param gusseingChars 控制台人工猜测字符序列数组
	 * @return new int[]{猜对字符的个数，猜对字符的位置个数}
	 */
	private static int[] checkChars(char[] randomChars, char[] gusseingChars){
		//随机数组、人工输入数组进行对比  start
		int rightNumber = 0;
		int rightIndex = 0;
		for(int i=0; i<randomChars.length; i++){//控制轮数
			for(int j=0; j<gusseingChars.length; j++){//控制每轮次数
				if(randomChars[i] == gusseingChars[j]){
					//猜对字母
					rightNumber ++;
					if(i == j){
						//猜对位置
						rightIndex ++;
					}
				}
			}
		}
		//随机数组、人工输入数组进行对比  end
		return new int[]{rightNumber,rightIndex};
	}
}
```

###质数判断输出
```
输入一个数，输出小于这个数的所有质数
package com.ksxx.corejava.day04.pm;

import java.util.Scanner;

public class LianXi10 {

	/**
	 * 质数
	 * @param args
	 */
	public static void main(String[] args) {
		System.out.println("请输入查找质数的范围2~");
		//获取质数范围2~num
		Scanner scan=new Scanner(System.in);
		int num=scan.nextInt();
		int count=0;//质数的计数
		//循环判断质数开始
		for(int i=2;i<=num;i++){
		    boolean flag=true;          
		    for(int j=2;j<=Math.sqrt(i);j++){
		    	if(i%j==0){
		    		flag=false;
		    		  break;
		    	}
		    }
		    //判断质数结束
		        if(flag){
		    		count++;
		        	System.out.print(i+" ");
		        	if(count%10==0){
		        		System.out.println();
		        	}
		    	}
		    }
	    System.out.println("\n共有"+count+"个质数");
	}
}
```
###冒牌排序
```
package com.ksxx.corejava.day07.pm;

import java.util.Arrays;

/**
 * 冒泡算法：
 * 	两两比较，大的后移。
 * 	每一轮冒出一个最大数，直到排序结束。
 * @author chengcheng
 *
 */
public class Demo01 {

	public static void main(String[] args) {
		int[] nums = {1,2,3,4,6,5};
		System.out.println("原数组："+Arrays.toString(nums));
		System.out.println("***********************start");
		
		for( int i=0; i<nums.length-1 ; i++){//外层循环控制行（轮数）
			System.out.println(nums.length+"个数，第"+(i+1)+"轮：");
		    for( int j=0; j<nums.length-i-1 ; j++){//内存循环控制列（每轮次数）
		    	//两两比较，大的后移
				if(nums[j]<nums[j+1]){
					int temp = nums[j+1];
					nums[j+1] = nums[j];
					nums[j] = temp;
				}
				System.out.println('\t'+"第"+(j+1)+"次结果："+Arrays.toString(nums));
		    }
		}
		System.out.println("***********************end");
		
		System.out.println("经过冒泡算法排序后数组："+Arrays.toString(nums));
	}
}
```
