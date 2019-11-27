
#### 1，关于密码输入错误
如果密码输入错误，则会提示：
java.sql.SQLException: Access denied for user 'root'@'localhost' (using password: YES),


#### 2，一次性插入100条数据

```
package jdbc;
   
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Statement;
   
public class TestJDBC {
    public static void main(String[] args) {
   
        try {
            Class.forName("com.mysql.jdbc.Driver");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
   
        try (
            Connection c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/how2java?characterEncoding=UTF-8",
                "root", "admin");
            Statement s = c.createStatement();             
        )
        {
        	for (Integer i = 0; i < 100; i++) {
        		String name="英雄"+i.toString();
        		String sql = "insert into hero values(null,"+"name"+","+313.0f+","+50+")";
        		s.execute(sql);

        		System.out.println("执行插入语句成功");
        	}

               
        } catch (SQLException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    }
}


```
* Out:
![](https://github.com/BinGYiZhanG/Java/blob/master/Java%E5%9F%BA%E7%A1%80/how2j/Images/jdbc1.jpg)
* 进一步订正
```
明显不符合题意（不会处理name部分）


for (Integer i = 0; i < 100; i++) {
  String sql = "insert into hero values(null, " + "'英雄" + i + "'" + ", " +  ((float)(300 + i)) + ", " +  (50 + i) + ")";
  ///相当于插入一条语句：
  ///(英雄i,300+i,50+i)
  s.execute(sql);

  System.out.println("执行插入语句成功");
}

```

















