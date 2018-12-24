JDBC：Java database connectivity
不同数据库厂商，会提供不同的架包，实现jdbc的一套接口标准
JDBC接口及数据库厂商实现
DriverManager   Connection  DatabaseMetaData  statemet ResultSet
工作原理：加载驱动建立连接，创建语句对象，执行SQL语句，处理结果集，关闭连接

加载驱动：
Class.forName("oracle.jdbc.diver.OracleDriver")
创建连接：
connection conn=DriverManager.getConnection("jdbc.oracle:thin:@IP:端口号：数据库名称"，“用户名” ，“密码”）；
获取连接：
Statement stmt=conn.createStatement();
执行sql语句 ：
stmt.executeUpdate(sql);
关闭语句对象，连接，释放资源
```
if(stmt!=null){
			stmt.close();
		}
if(conn!=null){
			conn.close();
		}
```

![stmt](http://upload-images.jianshu.io/upload_images/66256-6edee6577fd1422e.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

/**
 * JDBC 是Java访问各种数据库的解决方案，这套解决方案是用一套标准接口来实现
 * 即访问数据库的通用API（sun公司制定）而实现这些接口的类是由数据库厂商提供的
 * 我们总称这些为JdbcDriver（mysql driver， oracle Driver）
 * JDBC的工作原理：
 * 驱动程序：一组实现类，类中实现了接口的各种方法，在程序中调用的是接口，在运行时实际调用的是
 * 类中实现的方法（这是多态的一种体现形式）
 * JDBC执行过程：加载驱动→获取链接→创建语句对象，发送sql语句→执行sql，获取结果集→处理结果集→释放资源
 * @author itachi
 *
 */
/* 
 * 导入jar包：创建lib文件夹，复制jar文件
 * 右击→build path→add build path
 */
/*
 * 迭代结果集
 */

public class Demo6 {
	public static void main(String[] args) throws ClassNotFoundException, SQLException {
		String driverName="oracle.jdbc.driver.OracleDriver";
		String url="jdbc:oracle:thin:@localhost:1521:Orcl";
		String userName="itachi";
		String password="2649057";
		String sql="select id,name from t_user";
		Class.forName(driverName);//加载驱动
		Connection conn=DriverManager.getConnection(url, userName, password);//获取链接
		Statement stmt=conn.createStatement();//创建语句对象
		ResultSet rs=stmt.executeQuery(sql);//执行sql，获取结果集
		//移动指针，指向第一条记录，每执行一次就向下移动一次
		//移动结果集指针，返回boolean值，false表示没有记录，true表示有记录
/*		rs.next();
		//getXXX("colun_name")，返回对应字段值
		int id=rs.getInt("id");
		String name=rs.getString("name");
		System.out.println("编号\t姓名\n"+id+"\t"+name);*/
		
		//结果集为多条时，使用循环迭代结果
		while(rs.next()){
			int id=rs.getInt("id");
			String name=rs.getString("name");
			System.out.println("编号\t姓名\n"+id+"\t"+name);
		}
		if(stmt!=null){
			stmt.close();
		}
		if(conn!=null){
			conn.close();
		}
	}

}
```
