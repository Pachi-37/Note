[返回](../Mysql.md)

# 字符编码



##### 创建数据库设置字符编码

```mysql
create database if not exists `students` charset=utf8;
```



##### 查看数据库创建信息

```mysql
show create database [DatabaseName];
```



##### 修改数据库的字符编码

```mysql
alter database [DatabaseName] charset=utf8;
```



