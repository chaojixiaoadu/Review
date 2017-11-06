# MySQL

标签： 模拟面试

---
## 1、	说明一下数据库的事务概念.

    一个数据库事务通常包含对数据库进行读或写的一个操作序列。它的存在包含有以下两个目的：

> 1、为数据库操作提供了一个从失败中恢复到正常状态的方法，同时提供了数据库即使在异常状态下仍能保持一致性的方法。 
2、当多个应用程序在并发访问数据库时，可以在这些应用程序之间提供一个隔离方法，以防止彼此的操作互相干扰。

    事务应该具有4个属性：原子性、一致性、隔离性、持久性。这四个属性通常称为ACID特性。

* 原子性（Atomicity）：事务作为一个整体被执行，包含在其中的对数据库的操作要么全部被执行，要么都不执行。 
* 一致性（Consistency）：事务应确保数据库的状态从一个一致状态转变为另一个一致状态。一致状态的含义是数据库中的数据应满足完整性约束。 
* 隔离性（Isolation）：多个事务并发执行时，一个事务的执行不应影响其他事务的执行。 
* 持久性（Durability）：一个事务一旦提交，他对数据库的修改应该永久保存在数据库中。

## 2、	如何用select语句，查询获取一张表中，除了主键id不同，其余字段都相同的记录.

```
select * from `user`   
where `name`
in (select name from `user` Group By name having count(*) > 1)
and age
in (select age from `user` Group By age having count(*) > 1)
```

## 3、	Sql的统计函数有哪些？

> count()   统计记录条数，如 select count(*) from stu;
sum()  统计记录字段的和，如select sum(salary) from emp;
avg()  统计记录字段的平均值，如select avg(salary) from emp;
max() 查询字段中的最大值，如select max(age) from stu;
min() 查询字段中的最小值，如select min(age) from stu;

## 4、	Where、having有什么区别？

    where和having其实后面都是跟条件。
    区别在于：在他们后面的条件里如果有count之类的聚合函数的时候只能使用having而不能使用where。

## 5、	如何实现升序和降序查询？

    mySql中，升序为asc，降序为desc。

* 例如：

> 升序：select   *  from  表名 order by  表中的字段 asc(mysql中默认是升序排列，可不写);

> 降序：select   *  from  表名 order by  表中的字段 desc;

> 若要进行同时一个升序，一个降序，则如下：order by 升序字段 asc，降序字段 desc。

