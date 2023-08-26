# MySQL 学习

## 事务

介绍：事务是一系列操作的集合，不可分割的，会把所有操作放到一个整体像一起向系统提交或者撤销操作请求，这些操作**要么同时成功要么同时失败**

流程如下：

![image-20230804111736461](C:\Users\23882\AppData\Roaming\Typora\typora-user-images\image-20230804111736461.png)

```mysql
-- 方式一
select @@autocommit;    -- 将事务提交设置为手动提交
set @@autocommit =0;
-- 1.查询张三的账户余额
select * from account where name='张三';
-- 2.将张三的账户余额-1000
update account set money = money-1000 where name='张三';
-- 3.将李四的账户余额+1000
update account set money = money+1000 where name='李四';
-- 执行成功就提交事务
commit;
-- 执行失败就回滚事务
rollback;

-- 方式二
start transaction;	-- 不需要手动关闭自动提交事务了，改语句后的语句都是手动提交
-- 1.查询张三的账户余额
select * from account where name='张三';
-- 2.将张三的账户余额-1000
update account set money = money-1000 where name='张三';
-- 3.将李四的账户余额+1000
update account set money = money+1000 where name='李四';

commit ;

rollback ;
```



## 事务的特性ACID

- A (Atomicity) 原子性 ： 事务是不可分割的最小单元，要么全部成功，要么全部失败
- C(Consistency) 一致性：事务完成时，所有数据都保持一致状态
- I(Isolation) 隔离性：数据库提供的隔离机制，保证事务在不受外部并发操作的独立环境运行
- D(Durability)持久性 ：事务一旦提交和回滚，他对数据库中的数据改变是永久的

## 并发事务问题

- 脏读 一个事务读到另一个事务还没有提交的数据
- 不可重复读：一个事务读取同一条记录，但两次读取的数据不同，称之为不可重复读
- 幻读：一个事务查询数据，没有查询到，但插入数据时发现这个是数据已经存在了，好像出现了幻影

## 事务的隔离级别

| 隔离级别                   | 脏读 | 不可重复读 | 幻读 |
| -------------------------- | ---- | ---------- | ---- |
| Read uncommitted           | √    | √          | √    |
| Read committed             | ×    | √          | √    |
| Repeatable Read(MySQL默认) | ×    | ×          | √    |
| Serializable               | ×    | ×          | ×    |

```mysql
-- 查看事务隔离级别
SELECT @@TRANSACTION_ISOLATION
-- 设置事务隔离级别
SET [SESSION|GLOBAL] TRANSACTION ISOLATION LEVEL [READ UNCOMMITTED | READ COMMITTED |REPEATABLE READ|SERIALIZABLE]

-- 事务的隔离级别越高，数据越安全，但是性能越低
```

