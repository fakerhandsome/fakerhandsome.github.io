---
id=Leecode01
title=学习Leecode第一天
---

## 1. Mysql练习

#### 1. 上升的温度

#####     1.1 题目描述

SQL架构

表 `Weather`

```
+---------------+---------+
| Column Name   | Type    |
+---------------+---------+
| id            | int     |
| recordDate    | date    |
| temperature   | int     |
+---------------+---------+
id 是这个表的主键
该表包含特定日期的温度信息
```

 

编写一个 SQL 查询，来查找与之前（昨天的）日期相比温度更高的所有日期的 `id` 。

返回结果 **不要求顺序** 。

查询结果格式如下例：

```mysql
Weather
+----+------------+-------------+
| id | recordDate | Temperature |
+----+------------+-------------+
| 1  | 2015-01-01 | 10          |
| 2  | 2015-01-02 | 25          |
| 3  | 2015-01-03 | 20          |
| 4  | 2015-01-04 | 30          |
+----+------------+-------------+

Result table:
+----+
| id |
+----+
| 2  |
| 4  |
+----+
2015-01-02 的温度比前一天高（10 -> 25）
2015-01-04 的温度比前一天高（20 -> 30）
```

---

正确题解和思路：

```mysql
SELECT
	b.id 
FROM
	WEATHER AS a,
	WEATHER AS b 
WHERE
	a.temperature < b.temperature 
	AND DateDIFF( a.recordDate, b.recordDate )=-1
	
通过两张表进行查询温度的大小关系  关联  后用日期函数 DATEDIFF(exp1,exp2)-->日期的差值
差值为-1,即为隔天
---

SELECT
	w2.id 
FROM
	weather AS w1
	LEFT JOIN weather w2 ON DATE_ADD( w1.recordDate, INTERVAL 1 DAY )= w2.recordDate 
WHERE
	w1.temperature < w2.temperature
通过两张表的左外连接查询，on后面跟随的条件是DATE_ADD(date1,INTERVAL expr unit)=date2 也是日期函数的一种差值查询条件

重点隔天，用到了DATE_ADD，DATEDIFF 两个函数
```

---

#### 2. 部门工资最高的员工

`Employee` 表包含所有员工信息，每个员工有其对应的 Id, salary 和 department Id。

```java
+----+-------+--------+--------------+
| Id | Name  | Salary | DepartmentId |
+----+-------+--------+--------------+
| 1  | Joe   | 70000  | 1            |
| 2  | Jim   | 90000  | 1            |
| 3  | Henry | 80000  | 2            |
| 4  | Sam   | 60000  | 2            |
| 5  | Max   | 90000  | 1            |
+----+-------+--------+--------------+
```

`Department` 表包含公司所有部门的信息。

```java
+----+----------+
| Id | Name     |
+----+----------+
| 1  | IT       |
| 2  | Sales    |
+----+----------+
```

编写一个 SQL 查询，找出每个部门工资最高的员工。对于上述表，您的 SQL 查询应返回以下行（行的顺序无关紧要）。

---

正确题解和思路：

```mysql
SELECT
    Department.name AS 'Department',
    Employee.name AS 'Employee',
    Salary
FROM
    Employee
        JOIN
    Department ON Employee.DepartmentId = Department.Id
WHERE
    (Employee.DepartmentId , Salary) IN
    (   SELECT
            DepartmentId, MAX(Salary)
        FROM
            Employee
        GROUP BY DepartmentId
	)
;
思路:两张表的关联查询，通过分组获得表的两个字段，其中一个包含工资最高的字段，然后用in找到对应字段，用where条件查询就可以得到

---
官方讲解：
回忆一下 GROUP BY 语句


GROUP BY 字段名   # 根据字段进行分组
先对 DepartmentId 字段分组查询最大值，得到不同 DepartmentId 下的最大值


SELECT DepartmentId, max( Salary ) 
FROM Employee 
GROUP BY DepartmentId 
再根据 DepartmentId 字段连接 Department 表，根据 Salary 和 DepartmentId 查找 Department.Name 字段


SELECT
	Department.NAME AS Department,
	Employee.NAME AS Employee,
	Salary 
FROM
	Employee,
	Department 
WHERE
	Employee.DepartmentId = Department.Id 
	AND ( Employee.DepartmentId, Salary ) 
    IN (SELECT DepartmentId, max( Salary ) 
        FROM Employee 
        GROUP BY DepartmentId )
```

