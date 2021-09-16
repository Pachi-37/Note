# `Mysql`选修部分



# 视图

用来筛选数据，隐藏敏感数据

```mysql
CREATE[OR REPLACE] [ALGORITHM = {UNDEFINED | MERGE | TEMPTABLE}]
    VIEW view_name [(column_list)]
    AS select_statement
   [WITH [CASCADED | LOCAL] CHECK OPTION]
```



### 视图选择算法

- `undefined`
  - 默认选择的算法
- `merge`
  - 自动选择使用的算法
- `temptable`



### 视图权限

- `cascade`
  - 更新视图时，满足视图和表的相关条件
- `local`
  - 满足视图定义的一个条件
- `check option`
  - 推荐使用，保证数据安全性



# 事务

操作性严谨相关操作（钱）

网上购物钱

```mysql
# 开启事务
start transaction;

# 回滚
rollback;

# 提交事务
commit;

# 设置回滚点
savepoint [point];
rollback to point;
commit;
```



### ACID

- `atomicity`
  - 原子性
- `consistency`
  - 一致性
- `isolation`
  - 隔离性
- `durability`
  - 持久性



> 注：创建 `Mysql` 只有指定引擎为 `innodb` 时才可以使用



# 索引

帮助快速查找数据，但会导致 `CRUD` 效率降低，导致空间使用变大



##### 主键索引

##### 唯一键索引

##### 普通索引

##### 全文索引

- `sphinx` 可以解决中文索引问题



```mysql
create index indexName on table_name (column_name); 
```



> 经常查询的数据创建索引
>
> 公共字段法创建索引
>
> 数据过少不创建索引，



# 存储过程

模块化设计（函数）



```mysql
# 更改结束符 
delimiter //

# 创建存储过程
create procedure proc()
begin 

end

# 调用
call proc;
```

