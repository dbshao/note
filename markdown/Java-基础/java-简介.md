<small>
#####1、什么是java？为什么要学java？
为什么学
一句话：java很火
什么是java？
是一门高级编程语言。
高级语言？
电脑很笨，只能认识0、1的低级语言。

#####2、java的特点
 C也是高级编程语言，主要偏向于底层开发。
		java主要偏向于应用型开发。
java的特点：
		开源、安全
		跨平台、简单、面向对象
C是不跨平台。 
		windows、IOS、linux
QQ：c开发的
		   windows系统，windows版本的QQ
		   IOS系统，IOS版本的QQ
		   linux系统，linux版本的QQ
如果用java开发
		   只需要开发一个版本即可。
		   windows系统，使QQ运行在windows系统的java虚拟机中。
		   IOS系统，使QQ运行在IOS系统的java虚拟机中。
		   linux系统，使QQ运行在linux系统的java虚拟机中。
不同系统平台的java虚拟机，由sun公司提供。
windows、IOS、linux不同系统服务器分布：
	    pc机：个人电脑
	    服务器：处理大数据、部署应用的主机
	    手持终端：手机、pad、掌上电脑
	    嵌入式设备：除上述之外的具有cpu的设备。
IOS系统：
	    IOS设备（苹果电脑、ipad、苹果手机）
windows系统：
	    绝大多数pc机，少数服务器。
linux系统（分布最广的系统）：
	    除了上述两种设备之外的所有服务器都采用linux系统。
		linux系统特点：
	    开源、安全。
	    java符合linux的特点，两者一拍即合。



#####3、java几个概念及环境变量配置
  ###### 1）、几个概念
JDK：java开发工具包
		保证能够实现java开发的最小单元。
JDK = JRE + 开发工具（开发、运行等）
JRE：java运行环境
		保证能够实现java软件运行的最小单元。
JRE = JVM + 系统类库
JVM：java虚拟机
		真正用来运行java程序的。

  ###### 2）、环境变量
	很多软件都是安装版，在安装过程中，
	直接向注册表中写入支持软件运行的“环境”。
	（即：安装版可以不用手动配置环境变量）
step1：
	   官网下载jdk（1.6、1.7，学习阶段不建议使用1.8）
step2：
	   安装即可。
对于绿色版的jdk（免安装的），则需要手动配置环境变量。
	对于安装的，也可以手动配置。
配置如下：
	    JAVA_HOME：jdk的（安装）主目录
		如：D:\Tools\JavaSource\JDK\jdk1.7.0_01
 CLASSPATH：编译路径
		. ：表示当前文件夹。
		D:\Tools\JavaSource\JDK\jdk1.7.0_01\lib
两者之间用;分隔，如下：
		.;D:\Tools\JavaSource\JDK\jdk1.7.0_01\lib
 PATH：命令路径
		做一些java相关操作命名，如：编译、运行、打包....
		如：D:\Tools\JavaSource\JDK\jdk1.7.0_01\bin
注：D:\Tools\JavaSource\JDK为存放路径（每个人不同）。
		
注意：linux系统大小写敏感，必须全大写。
		windows系统大小写不敏感，大小写无所谓。
配置环境变量的步骤：
	我的电脑 → 右键 → 属性 → 高级系统设置	→ 环境变量
对于JAVA_HOME、CLASSPATH，要新建。
	    如：
		变量名：JAVA_HOME
		变量值：D:\Tools\JavaSource\JDK\jdk1.7.0_01
对于PATH，里面已经存在，编辑即可。
	    鼠标移到最后，加上;分隔，再添加PATH变量值。
验证环境变量
	打开cmd窗口，敲入java（帮助信息）或java -version（版本号）


######3、java的运行原理
借助于命令操作，cmd窗口（控制台）输出hello world。
来分析java的运行原理如下：
java源文件（创建HelloWorld.java）
	     ↓
	编译成字节码文件（HelloWorld.class）
	     ↓
	运行字节码文件
	
编译：javac HelloWorld.java
	      javac编译命令，java源文件的全名（包括.java后缀）。

运行：java HelloWorld
	      java运行命令，字节码文件名称（不包括.class后缀）。

#####4、使用Eclipse工具开发第一个java程序。
IDE：java开发工具
	     Eclipse
 MyEclipse
		为Eclipse中的插件，为了方便web项目开发。
eclipse33.rar
	     是eclipse，但已经将MyEclipse插件安装好了。
	     安装路径为D:盘。
		
工具介绍：
	双击打开eclipse工具。
	workspace：
		开发文件的存放路径。
三个部分：
	   第一部分：新建部分
	   第二部分：编辑部分
	   第三部分：运行结果展示部分

开发第一个java程序：
		控制台打印输出：hello world
开发步骤如下：
	step1：新建java项目
		第一部分 → 右键 → new → java project
src：java源文件的根目录。
step2：新建包
		目的：为了更加方便的管理java源文件。
		建包原则：
		    包名小写，
		    公司简称（倒着写）.功能包（越细越好）
			点为层次关系

 www.baidu.com
			com.baidu

www.krosorsoft.com
			com.krosorsoft

com.ksxx
选中src → 右键 → new → package

step3：新建类
		类就是java源文件
选中对应的包 → 右键 → new → class（类）
	
src下有java源文件
bin下有.class字节码文件
这个编译过程，是eclipse主动实时完成的。

step4：编辑java源文件。
		在第二部分，对java源文件进行编写。
		编写代码口诀：
		    类中写方法，方法中写代码。

注意：所有的符号都是英文符号。
			大括号、小括号、中括号
			双引号、单引号符号都是成对出现的。

step5：运行java程序
		第二部分 → 右键 → run as → Java Application
注：如果run as之后没有 Java Application
			说明你的main（一个类的入口方法）写错了

			public static void main(String[] args){

			}
			
console控制台中就会输出：
			hello world

>作业：
	非常快速的能够实现MyEclipse编写步骤。
		新建项目
		  ↓
		新建包
		  ↓
		新建类
		  ↓
		编写java代码
		  ↓
		运行java程序
