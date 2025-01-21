# SQL学习

##  1.数据定义语言（DDL）

- create database
  - 创建一个新的数据库
  - create database database_name
- drop database
  - 删除一个数据库
  - drop database database_name
- alter database
  - 修改数据库属性
  - alter database database_name options (options_name options_value)
- create table
  - 创建一个新的表
  - create table table_name (column1 datatype, column2 datatype, ……)
- drop table
  - 删除一个表
  - drop table table_name
- alter table
  - 修改表的结果，如添加列、删除或修改列
  - alter table table_name add|drop|modify column column_name datatype
- create index
  - 在表上创建一个索引
  - create index index_name on table_name (column_name)
- drop index
  - 删除一个索引
  - drop index index_name on table_name
- truncate table 
  - 删除表中的所有记录，但保留表结构
  - truncate table table_name
- rename table
  - 重命名一个表
  - rename table old_table_name to new_table_name

## 2.数据库操作语言（DML）

- select
  - 从数据库中查询数据
  - select column1,column2…… from table_name where condition
- insert into
  - 向表中插入新记录
  - insert into table_name (column1,column2,……) values (value1,value2,……)
- update
  - 更新表中的现有记录
  - update table_name set column1 = value1, column2 = value2, …… where condition
- replace into
  - 插入新纪录，如果记录存在，则替换它
  - replace into table_name (column1, column2, …… ) values (value1, value2, ……)

## 3.数据库查询语言（DQL）

- join
  - 结合连个或多个表的记录
  - `select a.*, b.* from table_a a inner join table_b b on a.common_field = b.common_field`
- subquery
  - 在另一个查询中嵌套一个查询
  - select column_name from table_name where column_name in (select column_name from another_table)
- union
  - 合并两个或多个select语句的结果集
  - select column_name(s) from table1 union select column_name(s) from table2
- group by
  - 根据一个或多个列对结果集进行分组
  - select column_name, count(*) from table_name group by column_name 
- having
  - 过滤group by后的结果
  - `select column_name,count(*) from table_name group by column_name having count(*) > value`
- order by
  - 对结果集进行排序
  - select column_name(s) from table_name order by column_name [ASC|DESC]
- limit
  - 限制返回的记录数
  - select column_name(s) from table_name limit number

## 4.数据控制语言（DCL）

- grant
  - 授予用户权限
  - `grant all privileges on database_name.* to 'username'@'host' identified by 'password'`
- revoke
  - 撤销用户权限
  - `revoke all privileges on database_name.* from 'username'@'host'`
- set password
  - 更改用户密码
  - `set password for 'username'@'host' = password('newpassword')`

## 5.事务处理

- start transaction
  - 开始一个事务
  - start transaction
- commit
  - 提交事务，保存更改
  - commit
- rollback
  - 回滚事务，撤销更改
  - rollback
- savepoint
  - 设置保存点，以便可以回滚到该点
  - savepoint savepoint_name
- rollback to savepoint
  - 回滚到指定的保存点
  - rollback to savepoint savepoint_name
- release savepoint
  - 删除保存点
  - release savepoint savepoint_name

## 6.备份与恢复

- mysqldump
  - 导出数据库或表的数据
  - mysqldump -u username -p database_name > backup_file.sql
- mysql
  - 导入备份数据到数据库中
  - mysql -u username -p database_name < backup_file.sql

## 7.其他常用命令

- show database
  - 显示所有数据库
  - show database
- use
  - 选择当前数据库
  - use database_name
- show tables
  - 显示当前数据库中的所有表
  - show tables
- describe
  - 显示表的结构
  - describe table_name
- explain
  - 解释sql查询的执行计划
  - explain select column_name(s) from table_name where condition
- show columns
  - 显示表中的列信息
  - show columns from table_name
- show index
  - 显示表中的索引信息
  - show index from table_name 
- show status
  - 显示mysql服务器的状态信息
  - show status
- show variables
  - 显示mysql服务器的系统变量
  - show variables
- show grants
  - 显示用户权限
  - `show grants for 'username'@'host'`
- show processlist
  - 显示当前mysql服务器的连接信息
  - show processlist
- flush privileges
  - 用户重新加载授权表（如mysql.user, mysql.db ,mysql.table_priv, mysql.column_priv 登）的权限信息，使其对这些表的更改立即生效，而无需重启mysql服务器
  - flush privileges 