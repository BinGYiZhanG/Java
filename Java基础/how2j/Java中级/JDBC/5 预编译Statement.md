
#### 1，练习-性能比较

* （1），Statement插入
```
插入结束,耗时16463毫秒

long start = System.currentTimeMillis();
            
for(Integer i=0;i<10000;i++){
	String name="英雄"+i.toString();
	String sql = "insert into hero values(null,"+"name"+","+313.0f+","+50+")";
	s.execute(sql);

	System.out.println("执行插入语句成功");

}

long end = System.currentTimeMillis();

System.out.printf("插入结束,耗时%d毫秒", end - start);


```

* （2），PreparedStatement插入
```
插入结束,耗时14832毫秒
public class TestJDBC {
	public static void main(String[] args) {
    	Connection c = null;//建立与数据库的Connection连接
    	Statement s = null;//Statement是用于执行SQL语句的，比如增加，删除
    	//初始化驱动

    	String sql = "insert into hero values(null,?,?,?)";
        try {
        	Class.forName("com.mysql.jdbc.Driver");
        	c = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/how2java?characterEncoding=UTF-8",
                "root", "root");
            s = c.createStatement();
            PreparedStatement ps = c.prepareStatement(sql);
            
            long start = System.currentTimeMillis();
            
            for(Integer i=0;i<10000;i++){
            	String name="英雄"+i.toString();
            	
            	
            	ps.setString(1, name);
                ps.setFloat(2, 313.0f);
                ps.setInt(3, 50);
                ps.execute();

            	System.out.println("执行插入语句成功");

            }
            
            long end = System.currentTimeMillis();
            
            System.out.printf("插入结束,耗时%d毫秒", end - start);
            
            
             
        } catch (ClassNotFoundException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        } catch (SQLException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        } finally {
            // 数据库的连接时有限资源，相关操作结束后，养成关闭数据库的好习惯
            // 先关闭Statement
            if (s != null)
                try {
                    s.close();
                } catch (SQLException e) {
                    // TODO Auto-generated catch block
                    e.printStackTrace();
                }
            // 后关闭Connection
            if (c != null)
                try {
                    c.close();
                } catch (SQLException e) {
                    // TODO Auto-generated catch block
                    e.printStackTrace();
                }
 /*
  数据库的连接是有限资源，相关操作结束后，养成关闭数据库的好习惯
先关闭Statement
后关闭Connection 
  */
        }
   
    }

}


```

