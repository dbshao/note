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
