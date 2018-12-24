与oracle不同是 在加载驱动的时候要用
Class.forName(driverName).newInstance();
其中的driverName用
 driverName =  "com.mysql.jdbc.Driver";
获取链接的时候用
Connection conn = DriverManager.getConnection(url);
其中的url用 
private static String url = "jdbc:mysql://ip地址:端口/数据库名称?user=用户名&password=密码&useUnicode=true&characterEncoding=utf-8";


JDBC工具类举例：
```
package util;

import java.io.IOException;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;
import java.util.Properties;

/*
 * JdbcUtil工具类
 * 封装jdbc中重复的内容
 * 1.加载驱动
 * 2.创建连接
 * 3.关闭资源
 */
public class JdbcUtil {
	private static String driverName=null;
	private static String userName=null;
	private static String password=null;
	private static String url=null;
	private JdbcUtil(){}
	
	
	static {
		try {
			Properties prop=new Properties();
			prop.load(JdbcUtil.class.getClassLoader().
					getResourceAsStream("db.properties"));
			driverName=prop.getProperty("driverName");
			url=prop.getProperty("url");
			userName=prop.getProperty("userName");
			password=prop.getProperty("password");
			//加载驱动
			Class.forName(driverName);
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
			throw new RuntimeException(e);
			
		} catch (IOException e) {
			e.printStackTrace();
			throw new RuntimeException(e);
		}
	}
	
	//建立连接
	public static  Connection getConnection() throws SQLException{
		Connection conn=DriverManager.
		           getConnection(url,userName,password);
		return conn;
	}
	
	//关闭连接
	public static void close(ResultSet rs, Statement stmt,Connection conn){
		
			try {
				if(rs!=null){
				rs.close();
				}
			} catch (SQLException e) {
			   e.printStackTrace();
			   throw new RuntimeException(e);
			}finally{
				
					try {
						if(stmt!=null){
						stmt.close();
						}
					} catch (SQLException e) {
						e.printStackTrace();
						throw new RuntimeException(e);
					}finally{
						try {
							if(conn!=null){
							 conn.close();
							}
						} catch (SQLException e) {
							e.printStackTrace();
							throw new RuntimeException(e);
						}
					}
			}
	}
	
	public static void main(String[] args) throws SQLException {
		Connection conn=JdbcUtil.getConnection();
		System.out.println(conn);
	}

}

```
