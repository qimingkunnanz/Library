#### 数据库基本操作

```sql
-- 表示单行注释   
/* 用于多行（块）注释  */
-- 一些基本的sql语句的使用
-- sql语句后面都要加上分号结尾
show databases; -- 查看所有的数据库
use mysql_001; -- 使用mysql_001 数据库
show tables; -- 查看所有表
desc users; -- 查看表结构
select * from users;
source e:/test/test.sql; -- 导入sql脚本，这才是工作里面常用的开发方式

-- 对表，数据库的处理
drop table users; -- 删除表， 啥都没有了  老大
truncate users; -- 清空表,自增的序列清0，表结构还在
delete table users; -- 删除内存，不删除定义，不释放空间，一行一行的删，效率比truncate低
```

1. SQL 也是一门语言，也有数据类型，初级先学习 增删改查

   ```sql
   --对数据的处理
   -- 1. 增加(插入数据)， 两种办法，一般用第一种
   insert into users (uname,age,gender) values ('张三', 26, '男');
   --自增的主键，一般可以不写
   insert into users (id,uname,age,gender) values (null,'张三', 26, '男');
   
   insert into users (uname,age,gender) select name, age, gender from account; -- 从一个表中查到数据后 在对应的添加进去
   
   -- 2. 删除
   delete from users where id = '2';
   
   -- 3. 改
   update users set age=99 where id = 1; -- 后面非数字要跟引号
   ```

2. sql的关键在于查询

   ```sql
   -- 4. 查
   -- 这个才是影响我们程序性能的关键， 一般的淘宝，等电商网站，买火车票网站，各种复杂的查询都是 数据库db 程序员做的事情， 不断的优化查询算法，让时间缩短，提高用户体验，更快的将结果返回给后端
   
   ---1. 查询部分行列， 生产环境一定不要用*
   select uname, age from users;
   select uname, age from users where id = 5;
   
   ---2. like模糊查询
   // 表示查询uname字段 第一个子为张的记录
   select uname,age,gender from users where uname like '张%';
   
   ---3. between， in 范围查询
   select uname from users where age between 10 and 30;
   select uname, age from users where age in (11,99);
   
   ---4. 分组查询
   -- 注意分组查询里面不能使用where语句， 要是有条件的话 需要用having
   select uname as '姓名' from users group by id;
   select uname as '姓名' from users group by id having count(age)>0;
   
   ---5. 多表级联查询
   select a.uname,b.account from a,b where a.id = b.id;
   ```


