事物操作：模拟银行转账系统
```
package day03;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;
/*
 * 事务演示：转账
 */

import day01.JdbcUtil;

public class Demo2 {
	public static void main(String[] args) {
		int outId=1001;
		int inId=1002;
		double money=1000;
		String outSql="update c_account set money=money-? where id=?";
		String inSql="update c_account set money=money+? where id=?";
		Connection conn=null;
		PreparedStatement pstmt=null;
		
		try {
			conn=JdbcUtil.getConnection();
			//设置自动提交方式为false
			conn.setAutoCommit(false);
			//转出
			pstmt=conn.prepareStatement(outSql);
			pstmt.setDouble(1, money);
			pstmt.setInt(2, outId);
			pstmt.executeUpdate();
			
			//转入
			pstmt=conn.prepareStatement(inSql);
			pstmt.setDouble(1,money);
			pstmt.setInt(2, inId);
			pstmt.executeUpdate();
			
			conn.commit();
			conn.setAutoCommit(true);
		
		} catch (SQLException e) {
			e.printStackTrace();
			try {
				conn.rollback();
			} catch (SQLException e1) {
				// TODO Auto-generated catch block
				e1.printStackTrace();
			}
		}finally{
			JdbcUtil.close(null, pstmt, conn);
		}
	}

}
```
批量处理：
```
package day03;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.sql.Statement;

import day01.JdbcUtil;

/*
 * 演示：JDBC的批量处理
 */

public class Demo3 {
	public static void main(String[] args) {
//		testInsert();
		int[] empNos=new int[30];
		int empNo=1209;
		for(int i =0;i<empNos.length;i++){
			empNos[i]=empNo;
			empNo-=5;
		}
		deleteByEmpNos(empNos);
	}
	//批量插入
	public static void testInsert(){
		Connection conn=null;
		Statement st=null;
		try {
			conn=JdbcUtil.getConnection();
			st=conn.createStatement();
			int count =1290;
			for(int i=0;i<=count;i++){
				String sql="insert into emp(empno,ename) values(empseq.nextval,'员工"+i+"')";
				//添加sql语句到语句对象的语句列表中
				st.addBatch(sql);
				if(i%200==0){
					//执行语句列表中的语句
					st.executeBatch();
					//清空语句列表中的sal
					st.clearBatch();
				}
			}
			//执行语句列剩下的sql
			st.executeBatch();
		} catch (SQLException e) {
			e.printStackTrace();
		}finally {
			JdbcUtil.close(null, st, conn);
		}
	}
	
	public static void deleteByEmpNos(int[] empNos){
		Connection conn=null;
		PreparedStatement ps=null;
		try {
			conn=JdbcUtil.getConnection();
			String sql="delete from emp where empno=?";
			ps=conn.prepareStatement(sql);
			for(int empNo: empNos){
				ps.setInt(1, empNo);
				ps.addBatch();
			}
			ps.executeBatch();
			ps.clearBatch();
		} catch (SQLException e) {
			e.printStackTrace();
		}finally{
			JdbcUtil.close(null, ps, conn);
		}
	}

}
```

