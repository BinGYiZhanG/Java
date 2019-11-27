### (1),没加try-catch()  ×
### (2),将try-catch()语句封装到另一个函数中，调用  ×
### (3),直接在main函数中调用数据库相关  √


* （1），这样写execute()函数是不行的，
```
public static void execute(String sql){
	Class.forName("com.mysql.jdbc.Driver");
	 ///没加try-catch()
	Connection c = DriverManager
			.getConnection(
					"jdbc:mysql://127.0.0.1:3306/how2java?characterEncoding=UTF-8",
					"root", "root");

	Statement s = c.createStatement();
	s.execute(sql);
}
```
* （2），这样写也是不行的，
```
public class TestJDBC {

	public static void execute(String sql){
        
 //将try-catch()语句封装到另一个函数中，调用
        try(Connection c = DriverManager.getConnection(
        		"jdbc:mysql://127.0.0.1:3306/how2java?characterEncoding=UTF-8", "root", "root");
            Statement s = c.createStatement();) {
 
            s.executeUpdate(sql);
 
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
	public static void main(String[] args) {
		try {
            Class.forName("com.mysql.cj.jdbc.Driver");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
        for (int i = 0; i < 100; i++) {
            String strDelete = "delete from hero where id = " + i;
            String strAdd = String.format("insert into hero value(null, '%s', %.0f, %d)", ("hero" + i), (500.0f + i), 30);
            String strUpdate = String.format("update hero set name = 'name 888' where id = 205");
            execute(strAdd);
        }
    }
 
}
```
### 不知道哪里存在问题

* （3），正解：

```
package jdbc;
   
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
   
public class TestJDBC {
	public static void main(String[] args) {
		try {
			//导入jar包
			Class.forName("com.mysql.jdbc.Driver");
		} catch (ClassNotFoundException e) {
			// TODO: handle exception
			e.printStackTrace();
		}
		try(
		Connection c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/how2java?characterEncoding=UTF-8",
				"root", "root");
			Statement s = c.createStatement();  
		)
		{
			//进行增加操作
			//String sql = "insert into hero values(null," + "'提莫'" + "," + 313.0f + "," + 50 + ")";
			String sql1 = "insert into hero values(null,"+"'gareen'"+","+313.0f+","+50+")";
			s.execute(sql1);
			 
			//进行删除操作
			String sql2 ="delete from  hero where id = 106 ";
			s.execute(sql2);
		 
			//进行修改操作
			String sql3 = "update hero set name = '提莫' where id =105 ";
			s.execute(sql3);
		}catch (SQLException e) {//这句必加
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}

}

```
