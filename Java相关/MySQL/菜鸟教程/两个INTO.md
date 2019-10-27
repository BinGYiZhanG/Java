### SQL SELECT INTO 语句(MySQL不支持)

### SQL INSERT INTO SELECT 语句

* 通过 SQL，您可以从一个表复制信息到另一个表。
* INSERT INTO SELECT 语句从一个表复制数据，然后把数据插入到一个已存在的表中。
* 目标表中任何已存在的行都不会受影响。
```

mysql> SELECT * FROM Websites;
+----+---------------+---------------------------+-------+---------+
| id | name          | url                       | alexa | country |
+----+---------------+---------------------------+-------+---------+
|  1 | Google        | https://www.google.cm/    |     1 | USA     |
|  2 | 淘宝             | https://www.taobao.com/   |    13 | CN      |
|  3 | 菜鸟教程             | http://www.runoob.com/    |  4689 | CN      |
|  4 | 微博             | http://weibo.com/         |    20 | CN      |
|  5 | Facebook      | https://www.facebook.com/ |     3 | USA     |
|  6 | stackoverflow | http://stackoverflow.com/ |     0 | IND     |
|  7 | baidu         | https://www.baidu.com/    |     4 | CN      |
|  8 | QQ APP        |                           |     0 | CN      |
|  9 | Weibo APP     |                           |     0 | CN      |
| 10 | taobao APP    |                           |     0 | CN      |
+----+---------------+---------------------------+-------+---------+
10 rows in set (0.00 sec)


只复制 QQ 的 APP 到 "Websites" 中：

mysql> INSERT INTO Websites (name, country)
    -> SELECT app_name, country FROM apps
    -> WHERE id=1;
Query OK, 1 row affected (0.00 sec)
Records: 1  Duplicates: 0  Warnings: 0

mysql> SELECT * FROM Websites;
+----+---------------+---------------------------+-------+---------+
| id | name          | url                       | alexa | country |
+----+---------------+---------------------------+-------+---------+
|  1 | Google        | https://www.google.cm/    |     1 | USA     |
|  2 | 淘宝             | https://www.taobao.com/   |    13 | CN      |
|  3 | 菜鸟教程             | http://www.runoob.com/    |  4689 | CN      |
|  4 | 微博             | http://weibo.com/         |    20 | CN      |
|  5 | Facebook      | https://www.facebook.com/ |     3 | USA     |
|  6 | stackoverflow | http://stackoverflow.com/ |     0 | IND     |
|  7 | baidu         | https://www.baidu.com/    |     4 | CN      |
|  8 | QQ APP        |                           |     0 | CN      |
|  9 | Weibo APP     |                           |     0 | CN      |
| 10 | taobao APP    |                           |     0 | CN      |
| 11 | QQ APP        |                           |     0 | CN      |
+----+---------------+---------------------------+-------+---------+
11 rows in set (0.00 sec)

```


#### [select into from 和 insert into select区别](https://www.runoob.com/sql/sql-insert-into-select.html)

