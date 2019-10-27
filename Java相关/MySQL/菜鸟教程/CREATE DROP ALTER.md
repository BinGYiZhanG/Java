
### SQL CREATE DATABASE 语句
```
mysql> CREATE DATABASE my_db;
Query OK, 1 row affected (0.01 sec)

mysql> use my_db;
Database changed

```
### SQL CREATE TABLE 语句  与  SQL 约束（Constraints）
#### SQL CREATE TABLE + CONSTRAINT 语法

#### ```NOT NULL - 指示某列不能存储 NULL 值。```
#### ```UNIQUE - 保证某列的每行必须有唯一的值。```
#### ```PRIMARY KEY - NOT NULL 和 UNIQUE 的结合。确保某列（或两个列多个列的结合）有唯一标识，有助于更容易更快速地找到表中的一个特定的记录。```
#### ```CHECK - 保证列中的值符合指定的条件。```
```
CREATE TABLE Persons2
(
    Id_P int NOT NULL,
    LastName varchar(255) UNIQUE,
    FirstName varchar(255) PRIMARY KEY,
    Address varchar(255) ,
    City varchar(255),
	CHECK (Id_P>0)
);

```

####  [FOREIGN KEY](https://www.runoob.com/sql/sql-foreignkey.html) - 保证一个表中的数据匹配另一个表中的值的参照完整性。
* 1,
```mysql
"Persons" 表中的 "P_Id" 列是 "Persons" 表中的 PRIMARY KEY。
"Orders" 表中的 "P_Id" 列是 "Orders" 表中的 FOREIGN KEY。

在 "Orders" 表创建时在 "P_Id" 列上创建 FOREIGN KEY 约束：

mysql> CREATE TABLE Persons
    -> (
    ->     P_Id int NOT NULL,
    ->     LastName varchar(255) NOT NULL,
    ->     FirstName varchar(255),
    ->     Address varchar(255),
    ->     City varchar(255),
    ->     PRIMARY KEY (P_Id)
    -> );
Query OK, 0 rows affected (0.01 sec)

mysql> CREATE TABLE Orders
    -> (
    -> O_Id int NOT NULL,
    -> OrderNo int NOT NULL,
    -> P_Id int,
    -> PRIMARY KEY (O_Id),
    -> FOREIGN KEY (P_Id) REFERENCES Persons(P_Id)
    -> );
Query OK, 0 rows affected (0.01 sec)
```
  * 2,ALTER TABLE 时的 SQL FOREIGN KEY 约束
```mysql
  mysql> CREATE TABLE Orders
    -> (
    -> O_Id int NOT NULL,
    -> OrderNo int NOT NULL,
    -> P_Id int,
    -> PRIMARY KEY (O_Id)
    -> );
Query OK, 0 rows affected (0.01 sec)

mysql> ALTER TABLE Orders
    -> ADD FOREIGN KEY (P_Id)
    -> REFERENCES Persons(P_Id);
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

  * 撤销 FOREIGN KEY 约束 --- 没学会（通过子句）

####  ```DEFAULT - 规定没有给列赋值时的默认值。```
* 1,CREATE TABLE 时的 SQL DEFAULT 约束
```
mysql> CREATE TABLE Persons4
    -> (
    ->     P_Id int NOT NULL,
    ->     LastName varchar(255) NOT NULL,
    ->     FirstName varchar(255),
    ->     Address varchar(255),
    ->     City varchar(255) DEFAULT 'Sandnes'
    -> );
Query OK, 0 rows affected (0.01 sec)

mysql> CREATE TABLE Orders2
    -> (
    ->     O_Id int NOT NULL,
    ->     OrderNo int NOT NULL,
    ->     P_Id int,
    ->     OrderDate date DEFAULT GETDATE()
    -> );
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'GETDATE()
)' at line 6
```


 * 2,当表被创建时，ALTER TABLE 时的 SQL DEFAULT 约束
```
mysql> CREATE TABLE Persons5
    -> (
    ->     P_Id int NOT NULL,
    ->     LastName varchar(255) NOT NULL,
    ->     FirstName varchar(255),
    ->     Address varchar(255),
    ->     City varchar(255)
    -> );
Query OK, 0 rows affected (0.01 sec)

mysql> ALTER TABLE Persons5
    -> ALTER City SET DEFAULT 'SANDNES';
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

* 撤销 DEFAULT 约束

```
mysql> ALTER TABLE Persons
    -> ALTER City DROP DEFAULT;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0
```


### SQL CREATE INDEX 语句（没实操查数据）
* CREATE INDEX 语句用于在表中创建索引。
* 在不读取整个表的情况下，索引使数据库应用程序可以更快地查找数据


### SQL 撤销索引、撤销表以及撤销数据库

* DROP DATABASE 语句
```
mysql> DROP DATABASE my_db;
Query OK, 6 rows affected (0.04 sec)
```

* TRUNCATE TABLE 语句
```
mysql> CREATE TABLE Persons5
    -> (
    ->     P_Id int NOT NULL,
    ->     LastName varchar(255) NOT NULL,
    ->     FirstName varchar(255),
    ->     Address varchar(255),
    ->     City varchar(255)
    -> );
Query OK, 0 rows affected (0.01 sec)

mysql> TRUNCATE TABLE Persons5;
Query OK, 0 rows affected (0.00 sec)

mysql> SELECT * FROM Person5;
ERROR 1146 (42S02): Table 'abc.person5' doesn't exist
mysql> SELECT * FROM Persons5;
Empty set (0.00 sec)
```

### SQL ALTER TABLE 语句

```
mysql> CREATE TABLE Persons
    -> (
    ->     P_Id int NOT NULL,
    ->     LastName varchar(255) NOT NULL,
    ->     FirstName varchar(255),
    ->     Address varchar(255),
    ->     City varchar(255)
    -> );
Query OK, 0 rows affected (0.01 sec)

mysql> ALTER TABLE Persons
    -> ADD DateOfBirth date;
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> ALTER TABLE Persons
    -> ALTER COLUMN DateOfBirth year;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'year' at line 2
mysql> ALTER TABLE Persons
    -> DROP COLUMN DateOfBirth;
Query OK, 0 rows affected (0.02 sec)
Records: 0  Duplicates: 0  Warnings: 0
```




















