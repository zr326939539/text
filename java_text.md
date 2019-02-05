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
#### DQL 数据查询语言 用来查询数据
#### DCL 数据控制语言 用来定义访问权限和安全级别
