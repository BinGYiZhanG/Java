### 1，184 部门工资最高的员工

#### （1），自己的错解：
```

Select d.Name Department,e.Name Employee,e.Salary Salary
From Employee As e Left Join Department As d
On e.DepartmentId = d.Id
Having e.Salary in 
(
    Select Max(e.Salary)
    From Employee As e Left Join Department As d
    On e.DepartmentId = d.Id
    Group By d.Id
)
Order By d.Id

Out:

```
* 问题：输出排序问题
![](https://github.com/BinGYiZhanG/Java/blob/master/Java%E7%9B%B8%E5%85%B3/MySQL/Images/mysql4.jpg)


#### （2），正解
* 用```Where```进行筛选即可

```
select 
    d.Name as Department,
    e.Name as Employee,
    e.Salary 
from 
    Employee e,Department d 
where
    e.DepartmentId=d.id 
    and
    (e.Salary,e.DepartmentId) in (select max(Salary),DepartmentId from Employee group by DepartmentId);


```

### 2，185 部门工资前三高的所有员工
* 问题：不会分组求每个部门第三高的工资
```
Select d.name as Department,e.name as Employee,e.salary as Salary 
From employee as e Inner Join department as d 
On e.DepartmentId = d.id 
Where (
	Select Count(Distinct salary)  -- 同一个部门下，
	From employee 
	Where salary > e.salary And departmentid = e.DepartmentId 
) < 3 
Order By e.departmentid,Salary desc

看不懂
```

### 3，176 第二高的薪水
* 1，首先先将数据去重：
```
SELECT DISTINCT Salary 
FROM Employee
```
* 2，再将是数据按薪水降序排除：
```
SELECT DISTINCT Salary 
FROM Employee 
ORDER BY Salary DESC
```
* 3，分页的思想是一页一条数据，第二高的薪水则在第二页：
```
SELECT DISTINCT Salary 
FROM Employee 
ORDER BY Salary DESC 
LIMIT 1, 1
```
* 4，考虑到极端情况：没有第二薪水则为空，使用ifnull判断：
* 5，
```
SELECT IFNULL( 
        (
            SELECT DISTINCT Salary 
            FROM Employee 
            ORDER BY Salary DESC 
            LIMIT 1, 1
        )
        ,
            null) AS SecondHighestSalary
```
* 6，分页的其他使用：offset
* 7，SQL查询语句中的 ```limit``` 与 ```offset``` 的区别：
* 8，```limit y ```分句表示: 读取 y 条数据
* 9，```limit x, y ```分句表示: 跳过 ```x``` 条数据，读取 ```y``` 条数据
* 10，```limit y offset x``` 分句表示: 跳过 ```x``` 条数据，读取 ```y``` 条数据


### 4，601 体育馆的人流量
![](https://github.com/BinGYiZhanG/Java/blob/master/Java%E7%9B%B8%E5%85%B3/MySQL/Images/mysql1911281018.jpg)
![](https://github.com/BinGYiZhanG/Java/blob/master/Java%E7%9B%B8%E5%85%B3/MySQL/Images/mysql1911281019.jpg)


```

明明有6种排列：
Select Distinct a.*
From stadium As a,stadium As b,stadium As c
Where (
    (a.id = b.id - 1 And b.id + 1 = c.id) Or -- a,b,c
    (b.id = a.id - 1 And a.id + 1 = c.id) Or -- b,a,c 
    (a.id = c.id - 1 And c.id + 1 = b.id) Or -- a,c,b
    
    (b.id = c.id - 1 And c.id + 1 = a.id) Or -- b,c,a
    (c.id = a.id - 1 And a.id + 1 = b.id) Or -- c,a,b 
    (c.id = b.id - 1 And b.id + 1 = a.id)  -- c,b,a
    )   
And (a.people >= 100 And b.people >= 100 And c.people >= 100)
Order By a.id;

```

### 5，596 超过5名学生的课
* 错误代码：
```
Select class
From courses
Group By class
Having Count(*) >= 5

```

* 正解：对学生去重
```
Select class
From courses
Group By class
Having Count(Distinct Student) >= 5
```

### 6,177 第N高的薪水
```
Select(
          If(
              (Select Count(*) -- 薪水总个数得大于N，才能够选择第N高的薪水
              From(
                  Select Distinct e.Salary
                  From Employee As e
              ) As e) >= N,
              (
                  Select Min(e.Salary) -- 在这N个薪水中，选择最低的薪水就是，第N高的薪水
                  From(
                      Select Distinct e.Salary
                      From Employee As e
                      Order By e.Salary Desc -- 按照薪水降序排列，选出前N个薪水
                      Limit N
                  ) As e
              ) ,
              Null
          )
      )


````

* [If用法](https://www.cnblogs.com/baizhanshi/p/9284782.html)

![](https://github.com/BinGYiZhanG/Java/blob/master/Java%E7%9B%B8%E5%85%B3/MySQL/Images/mysql1911281022.jpg)
![](https://github.com/BinGYiZhanG/Java/blob/master/Java%E7%9B%B8%E5%85%B3/MySQL/Images/mysql1911281023.jpg)




