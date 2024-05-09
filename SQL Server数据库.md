新建数据库：

```sql
create database 数据库名;
```

新建表：

```sql
create table 表名(
	字段1 类型 约束,
    字段2 类型 约束,
    ....
    字段n 类型 约束
)
```



## 表操作

> [!tip]
>
> 对表操作前，都要写上代码：
>
> ```sql
> alter table 表名
> ```

修改表名：
```sql
exec sp_rename 'newbook','books';
```

增加字段：

```sql
alter table 表名
	add 字段 字段类型 约束
```

删除字段：

```sql
alter table 表名
	drop column 列名
```

修改字段类型：

```sql
alter table 表名
	alter column 字段名 新类型
```

修改字段名称：`exec sp_rename ''表名.字段名','新表名','column'`

## 数据操作

**新增数据：**

1. 为所有字段添加：

```sql
insert into 表名 
	values(值1,...,值n)
```

2. 为指定字段添加：

```sql
insert into 表名 (字段1,...,字段n)
	values(值1,...,值n)
```

**更新数据：**

```sql
update 表名 set 列名 = ...[where 条件]
```

**删除数据：**

```sql
delete from 表名 [where 条件]
```

> [!tip]
>
> 1. `where`为可选项
> 2. **删除数据时，如果不添加条件，则会删除所有数据。**
> 3. ***有依赖关系（外键约束）要先删除子表中的数据***

---

## 常用方法

**排序方法：**

```sql
order by COUNT(*) ASC    -- 升序
order by COUNT(*) DESC  -- 降序
```

**选取前n个：**

```sql
SELECT TOP 1  ....    -- 选取第一名
SELECT TOP N ....     -- 选取前n名
```

**模糊匹配：**

```sql
where reader_name LIKE '张%'   -- 选取读者姓名中性张的人
where reader_name LIKE '张_'     -- 选取读者姓名中姓张的，名字是两个字的人
where reader_name LIKE '张__'   -- 选取读者姓名中姓张的，名字是三个字的人
```

**内连接：**

```sql
books inner join readers   -- 使用内连接，连接books表以及readers表
books outer join readers   -- 使用
```



