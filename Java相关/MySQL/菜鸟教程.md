#### [菜鸟教程SQL](https://www.runoob.com/sql/sql-tutorial.html)
* 如何导入```websites.sql```和```access_log.sql  ```
  * 得用MySQL的客户端，导入（```.sql```文件用英文写，不然有乱码）
  ```
  create database abc;
  use abc;
  set names utf8;
  source C:XXXX\access_log.sql
  source C:XXXX\websites.sql
  ```
 * 对于每次重新启动MySQL客户端，
 ```
  create database abc;#去掉这行
  use abc;
  set names utf8;
  source C:XXXX\access_log.sql
  source C:XXXX\websites.sql
  ```
 
* 如何退出```MySQL```的```->```,用```;```
* [MySQL如何显示汉字](https://www.cnblogs.com/lfxiao/p/10550558.html)
  * ```set character_set_results=gb2312; ```
  
* 表的插入两个 ??
```
mysql> INSERT INTO Websites (name, url, alexa, country) ;
    -> VALUES ('baidu','https://www.baidu.com/','4','CN');
mysql> INSERT INTO Websites (name, url, country)
    -> VALUES ('stackoverflow', 'http://stackoverflow.com/', 'IND');
```
* SQL FULL OUTER JOIN 实例
```
MySQL中不支持 FULL OUTER JOIN，你可以在 SQL Server 测试以下实例。
SELECT Websites.name, access_log.count, access_log.date
FROM Websites
FULL OUTER JOIN access_log
ON Websites.id=access_log.site_id
ORDER BY access_log.count DESC;

```

* 创建新表```APP```,```apps```
```

CREATE TABLE APP
(
APPID int,
name varchar(255),
url varchar(255),
alexa varchar(255),
Country varchar(255)
);


INSERT INTO APP (name, url, alexa, country)
VALUES ('QQ APP','https://im.qq.com/','4','CN');


INSERT INTO APP (name, url, alexa, country)
VALUES ('weibo APP','https://weibo.com/','4','CN');

INSERT INTO APP (name, url, alexa, country)
VALUES ('taobao APP','https://www.taobao.com/','4','CN');

```

```
mysql> CREATE TABLE apps
    -> (
    -> id int,
    -> app_name varchar(255),
    -> url varchar(255),
    -> Country varchar(255)
    -> );
Query OK, 0 rows affected (0.01 sec)

mysql> INSERT INTO apps (id,app_name, url, country)
    -> VALUES ('1','QQ APP','https://im.qq.com/','CN');
Query OK, 1 row affected (0.00 sec)

mysql>
mysql> INSERT INTO apps (id,app_name, url, country)
    -> VALUES ('2','Weibo APP','https://weibo.com/','CN');
Query OK, 1 row affected (0.00 sec)

mysql>
mysql> INSERT INTO apps (id,app_name, url, country)
    -> VALUES ('3','taobao APP','https://www.taobao.com/','CN');
Query OK, 1 row affected (0.00 sec)

mysql> SELECT * FROM apps;
+------+------------+-------------------------+---------+
| id   | app_name   | url                     | Country |
+------+------------+-------------------------+---------+
|    1 | QQ APP     | https://im.qq.com/      | CN      |
|    2 | Weibo APP  | https://weibo.com/      | CN      |
|    3 | taobao APP | https://www.taobao.com/ | CN      |
+------+------------+-------------------------+---------+
3 rows in set (0.00 sec)

```


* 删除表的列属性
```
ALTER TABLE APP
DROP COLUMN City;

当删除表中的最后一个数据时，会出现如下
ERROR 1090 (42000): You can't delete all columns with ALTER TABLE; use DROP TABLE instead

```

* 修改表```APP```的列属性的数据类型（原因：无法插入汉字，想改变数据类型）
```
mysql> ALTER TABLE APP
    -> ALTER COLUMN name TEXT;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'TEXT' at line 2

```

* SQL SELECT INTO 语句

```
MySQL 数据库不支持 SELECT ... INTO 语句，但支持 INSERT INTO ... SELECT 。
SELECT INTO 语句可用于通过另一种模式创建一个新的空表。只需要添加促使查询没有数据返回的 WHERE 子句即可：

mysql> SELECT name, url
    -> INTO WebsitesBackup2016
    -> FROM Websites;
ERROR 1327 (42000): Undeclared variable: WebsitesBackup2016



```






