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



```
















