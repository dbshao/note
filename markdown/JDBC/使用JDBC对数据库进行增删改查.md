在用Java对数据库进行链接的时候我们需要运用到面向对象的方法，将数据库中的信息封装成一个对象，下面进行演示：

建立与员工表相对应的emp类
```
package day02;

import java.io.Serializable;
import java.sql.Date;

public class Emp implements Serializable {
	private Integer empNo;
	private String ename;
	private String job;
	private double sal;
	private double comm;
	private Date hiredate;
	private Integer deptNo;
	private Integer mgr;
	
	public Emp() {
	}

	public Emp(String ename, String job, double sal, double comm,
			Date hiredate, Integer deptNo, Integer mgr) {
		super();
		this.ename = ename;
		this.job = job;
		this.sal = sal;
		this.comm = comm;
		this.hiredate = hiredate;
		this.deptNo = deptNo;
		this.mgr = mgr;
	}

	public Emp(Integer empNo, String ename, String job, double sal,
			double comm, Date hiredate, Integer deptNo, Integer mgr) {
		super();
		this.empNo = empNo;
		this.ename = ename;
		this.job = job;
		this.sal = sal;
		this.comm = comm;
		this.hiredate = hiredate;
		this.deptNo = deptNo;
		this.mgr = mgr;
	}

	public Integer getEmpNo() {
		return empNo;
	}

	public void setEmpNo(Integer empNo) {
		this.empNo = empNo;
	}

	public String getEname() {
		return ename;
	}

	public void setEname(String ename) {
		this.ename = ename;
	}

	public String getJob() {
		return job;
	}

	public void setJob(String job) {
		this.job = job;
	}

	public double getSal() {
		return sal;
	}

	public void setSal(double sal) {
		this.sal = sal;
	}

	public double getComm() {
		return comm;
	}

	public void setComm(double comm) {
		this.comm = comm;
	}

	public Date getHiredate() {
		return hiredate;
	}

	public void setHiredate(Date hiredate) {
		this.hiredate = hiredate;
	}

	public Integer getDeptNo() {
		return deptNo;
	}

	public void setDeptNo(Integer deptNo) {
		this.deptNo = deptNo;
	}

	public Integer getMgr() {
		return mgr;
	}

	public void setMgr(Integer mgr) {
		this.mgr = mgr;
	}

	@Override
	public String toString() {
		return "Emp [empNo=" + empNo + ", ename=" + ename + ", job=" + job
				+ ", sal=" + sal + ", comm=" + comm + ", hiredate=" + hiredate
				+ ", deptNo=" + deptNo + ", mgr=" + mgr + "]"+"\n";
	}
	

	//给出主键的hashCode和equals方法

	@Override
	public int hashCode() {
		final int prime = 31;
		int result = 1;
		result = prime * result + ((empNo == null) ? 0 : empNo.hashCode());
		return result;
	}

	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		Emp other = (Emp) obj;
		if (empNo == null) {
			if (other.empNo != null)
				return false;
		} else if (!empNo.equals(other.empNo))
			return false;
		return true;
	}
}
```

insert语句对应的方法
```
	public void save(Emp emp){
		String sql="insert into emp values(empseq.nextval,?,?,?,?,?,?,?)";
		Connection conn=null;
		PreparedStatement pstmt=null;
		try {
			conn=JdbcUtil.getConnection();
			pstmt=conn.prepareStatement(sql);
			pstmt.setString(1,emp.getEname());
			pstmt.setString(2,emp.getJob());
			pstmt.setInt(3, emp.getMgr());
			pstmt.setDate(4, emp.getHiredate());
			pstmt.setDouble(5, emp.getSal());
			pstmt.setDouble(6,emp.getComm());
			pstmt.setInt(7,emp.getDeptNo());
			//执行
			pstmt.executeUpdate();
			
		} catch (SQLException e) {
			e.printStackTrace();
			throw new RuntimeException(e);
		}finally{
			JdbcUtil.close(null, pstmt, conn);
		}
	}
```
delete 语句对应的方法
```
	public void delete(Integer empno){
		String sql="delete from emp where empno=?";
		Connection conn=null;
		PreparedStatement ps=null;
		try {
			conn=JdbcUtil.getConnection();
			ps=conn.prepareStatement(sql);
			ps.setInt(1, empno);
			ps.executeUpdate();
		} catch (SQLException e) {
			e.printStackTrace();
			throw new RuntimeException("根据员工编号删除失败",e);
		}finally{
			JdbcUtil.close(null, ps, conn);
		}
	}
```
update语句对应的方法
```
public void update(Emp emp,Integer empno){
		String sql="update emp set ename=?, job=?," +
				"mgr=?,hiredate=?,sal=?,comm=?,deptno=?where empno=?";
		Connection conn=null;
		PreparedStatement pstmt=null;
		try {
			conn=JdbcUtil.getConnection();
			pstmt=conn.prepareStatement(sql);
			pstmt.setString(1,emp.getEname());
			pstmt.setString(2,emp.getJob());
			pstmt.setInt(3, emp.getMgr());
			pstmt.setDate(4, emp.getHiredate());
			pstmt.setDouble(5, emp.getSal());
			pstmt.setDouble(6,emp.getComm());
			pstmt.setInt(7,emp.getDeptNo());
			pstmt.setInt(8, empno);
			//执行
			pstmt.executeUpdate();
			
		} catch (SQLException e) {
			e.printStackTrace();
			throw new RuntimeException(e);
		}finally{
			JdbcUtil.close(null, pstmt, conn);
		}
	}
```
select语句
```
public Emp selectByempNo(Integer empNo){
		String sql="select * from emp where empno=?";
		Connection conn=null;
		PreparedStatement ps=null;
		ResultSet rs=null;
		Emp emp=new Emp();
		try {
			conn=JdbcUtil.getConnection();
			ps=conn.prepareStatement(sql);
			ps.setInt(1,empNo);
			rs=ps.executeQuery();
			while(rs.next()){
				emp.setComm(rs.getDouble("comm"));
				emp.setDeptNo(rs.getInt("deptno"));
				emp.setEname(rs.getString("ename"));
				emp.setHiredate(rs.getDate("hiredate"));
				emp.setJob(rs.getString("job"));
				emp.setMgr(rs.getInt("mgr"));
				emp.setSal(rs.getDouble("sal"));
				emp.setEmpNo(empNo);
			}
		} catch (SQLException e) {
			e.printStackTrace();
			throw new RuntimeException(e);
		}finally{
			JdbcUtil.close(rs, ps, conn);
		}
		
		return emp;
	}
	
```
查询所有员工信息
```
public List<Emp> selectAll(){
		String sql="select * from emp";
		Connection conn=null;
		PreparedStatement ps=null;
		ResultSet rs=null;
		List<Emp> list= new ArrayList<Emp>();
		
		try {
			conn=JdbcUtil.getConnection();
			ps=conn.prepareStatement(sql);
			rs=ps.executeQuery();
			while(rs.next()){
				Emp emp=new Emp();
				emp.setComm(rs.getDouble("comm"));
				emp.setDeptNo(rs.getInt("deptno"));
				emp.setEname(rs.getString("ename"));
				emp.setHiredate(rs.getDate("hiredate"));
				emp.setJob(rs.getString("job"));
				emp.setMgr(rs.getInt("mgr"));
				emp.setSal(rs.getDouble("sal"));
				emp.setEmpNo(rs.getInt("empno"));
				list.add(emp);
			}
		} catch (SQLException e) {
			e.printStackTrace();
			throw new RuntimeException(e);
		}finally{
			JdbcUtil.close(rs, ps, conn);
		}
		
		return list;
		
	}
	
```
查询某部门中最高工资的员工信息
```
//查询某部门中工资最高的员工信息
	//select max(sal) from emp where deptno=?
	//select * frm emp where sal=(select max(sal) from emp where deptno=?)
	public Emp findMaxSal(int deptNo){
		String sql="select * from emp where sal=(select max(sal) from emp where deptno=?)";
		Connection conn=null;
		PreparedStatement ps=null;
		ResultSet rs=null;
		Emp emp=new Emp();
		try {
			conn=JdbcUtil.getConnection();
			ps=conn.prepareStatement(sql);
			ps.setInt(1,deptNo);
			//执行
			rs=ps.executeQuery();
			while(rs.next()){
				emp=empMap(rs);
			}
			
		} catch (SQLException e) {
			e.printStackTrace();
			throw new RuntimeException(e);
		}finally{
			JdbcUtil.close(null, ps, conn);
		}
		return emp;
		
	}
```



