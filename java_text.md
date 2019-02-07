### Java 笔记
### MYSQL笔记
1. 表：具有固定的列数，和任意的行数
2. 数据库：数据库是一些关联表的集合
3. 列：一个数据项字段
4. 行：一条记录
5. 主键：主键是唯一的，一个数据表只能包含一个主键。可以使用主键来查询数据
6. 外键：关联两个表
7. 索引：

MYSQL：关系型数据库管理系统
MYSQL查看数据库：show databases;
information_schema：存储数据库对象信息
performance_schema：存储数据库服务器性能参数信息
mysql：存储数据库用户权限信息
sys：通过这个库可以快速的了解系统的元数据信息

创建数据库： create database + 数据库名字;
删除数据库：drop database + 数据库名字;
使用数据库： use 数据库名字;
查看数据库当中有多少张表：show tables;


数据库字符集 UTF-8

MYSQL存储引擎
事务：完全执行或完全不执行


MYISAM：既不支持事务，也不支持外键，尤其是访问速度快，对事务完整性没有要求或者以select,insert为主的应用基本都可以使用这个引擎来创建表
        每个MyISAM在磁盘上存储成3个文件，其中文件名和表名都相同，但是扩展名分别为 frm存储表定义 myd存储数据 myi 存储索引
        
INNODB: InnoDB存储引擎提供了具有提交，回滚和崩溃恢复能力的事务安全，但是对比MyISAM的存储引擎，InnoDB写的处理效率差一些并且会占用更多的磁盘空间以保留数据和索引

SQL常用数据类型
double double(5,2)表示最多5位，其中有2位小数
char 
varchar 可变长度字符串类型
text 字符串类型
blob 二进制类型
date 日期类型 yyyy-MM-dd
time 时间类型 hh:mm:ss
datetime 日期时间类型 yyyy-MM-dd hh:mm:ss

#### DDL 数据定义语言 用来定义数据库对象：创建库，表，列等。
查看表结构: desc 表名;
创建数据库：create database 数据库名 character set utf8;
创建表： create table 表名（列名 数据类型（如果是char类型需要注明字符串长度））;
e.g. create table students (id int, name varchar(255),age int, email varchar(255));
添加一列： ALTER TABLE 表名 ADD 列名 数据类型;
修改字段类型： ALTER TABLE 表名 MODIFY 列名 数据类型;
删除一列：ALTER TABLE 表名 DROP 列名;
修改表名： RENAME TABLE 原始表名 TO 要修改的表名;
查看表的创建细节：show create table 表名;
修改表的字符集: ALTER TABLE 表名 character set 字符集名称;
修改表的列名: ALTER TABLE CHANGE 原始列名 新列名 数据类型;
删除表: DROP TABLE 表名;
#### DML 数据操纵语言 用来操作数据库表中记录
查询表中数据：select * from 表名;
插入操作： insert into 表名 (列名1，列名2,...) values (列值1,列值2...);
更新操作：update 表名 set 列名1=列值1，列名2=列值2。。。where 列名=值
修改数据库密码：
use mysql;
update user set password=password('abc') WHERE User='root' and Host='localhost';
flush privileges; 刷新mysql的系统权限表

mysqladmin -u root -p password 1234

删除操作：
delete from 表名 where 列名=值;  删除指定数据或所有数据，数据可以找回
truncate table 表名; 把表直接drop掉，然后再创建一个同样的新表，数据不能找回
#### DQL 数据查询语言 用来查询数据
查询所有列：select * from 表名;
结果集：通过查询语句查询出来的数据以表的形式展示我们称这个表为虚拟结果集，存放在内存中。查询返回的结果是一张虚拟表。

查询指定的列：select 列名1，列名2... from 表名;

条件查询：条件查询就是在查询时给出where 字句，在where字句中可以使用一些运算符及关键字；
关键字及运算符： =，!=,<,>,<=,>=
               between ... and 值在什么范围
               in (set) 固定的范围值
               is null; is not null; （为空或不为空）
               and
               or
               not
性别为男，年龄为20         SELECT * from students where age=20 AND gender='男';
学号为1001或者名为zs的记录 SELECT * from students where id=1001 OR name='zs';
查询学号为1001,1002,1003的记录 SELECT * from students where id in (1001,1002,1003);
查询年龄为null的记录 SELECT * from students where age is null;
查询性别非男的记录 SELECT * from students where gender != '男';
查询年龄在18到20之间的记录 SELECT * from students where age BETWEEN 18 AND 20; 
SELECT * from students where age >= 18 AND age <= 20; 

模糊查询：
根据指定的关键字查询
使用LIKE关键字后跟通配符

查询姓名为五个字母构成的学生记录  SELECT * from students where name LIKE '_____'; 五个下划线
查询姓名为五个字母构成的学生记录 第五个字母为s SELECT * from students where name LIKE '____s';
查询以'm'开头的学生记录  SELECT * from students where name LIKE 'm%';
查询以第二个字母是'u'的学生记录  SELECT * from students where name LIKE '_u%';
查询姓名中包含's'的学生记录 SELECT * from students where name LIKE '%s%';
通配符  _ 任意一个字符
       % 任意多个字符

字段控制查询
        去除重复记录 select distinct (列名) from 表名
        把查询的结果进行运算 select *,列名1+列名2 from 表名; 
        IFNULL(exp1,exp2) 如果exp1字段为null，就把其值设为exp2
        对查询结果起名 select *,列名1+列名2 AS 别名 from 表名; 
        
 排序
        使用关键字ORDER BY
        升序 ASC 从小到大（默认）
        降序 DESC 从大到小  
        select * from employee order by salary asc;
        select * from employee order by salary desc, id desc;
        
 聚合函数 
        对查询结果进行统计计算
        count：统计指定列不为null的记录行数 
        select count(*) from employees;
        select count(*) from employee where salary > 2500;
        select count(*) from employee where IFNULL(salary,0)+IFNULL(performance,0) > 5000;
        
        max：计算指定列最大值 
        select max(salary) from employee;
        
        min：计算指定列最小值 
        select min(salary) from employee;
        
        sum：计算指定列和
        select sum(salary) from employee;
        select sum(salary),sum(performance) from employee;
        select sum(salary+IFNULL(performance,0)) from employee;
        
        avg：计算指定列平均值
        select avg(salary) from employee;
        
分组查询
        字段值相同的归为一组 group by
        当group by 单独使用时，只显示每组的第一条记录
        select * from employee group by gender;
        select department,group_concat(name) from employee group by department;
        select后面跟着的字段一般也跟在group by 后面
        select gender,name from employee group by gender,name;
        select gender,group_concat(name) from employee group by gender;
        select department,sum(salary) from employee group by department;
        在group by 后面的条件需要使用Having
        SELECT department,GROUP_CONCAT(salary),sum(salary) from employee group by department HAVING SUM(salary)>=9000;
        HAVING是在分组后对数据进行过滤，WHERE是在分组前对数据进行过滤，HAVING后面可以使用聚合函数，WHERE后面不可以使用聚合函数
        
        书写顺序
        select + from + where + group by + having + order by + limit
        
        Limit 用法 指定从哪个位置开始，一次查多少数据
        limit 参数1，参数2 参数1：从哪一行开始查 参数2：查多少条数据
        
        
#### DCL 数据控制语言 用来定义访问权限和安全级别
