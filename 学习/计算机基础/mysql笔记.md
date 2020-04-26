[TOC]



## 常用命令

+ `show databases;`
+ `show warnings;`
+ `show create databases name;`
  + ![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-02-05_10-26-44.png)

+ select database();



## 常用参数

- ![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-02-05_09-45-49.png "常用参数")

## 修改提示符

+ 登录时
  + mysql -uroot -proot --prompt 提示符

+ 登录后
  + prompt 提示符

+ prompt常用参数
  + ![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-02-05_09-51-05.png)

## mysql 语句规范

+ 关键字与函数名称全部大写
+ 数据库名称、表名称、字段名称小写
+ sql语句必须以分号结尾

## 登陆数据库

+ mysql -u root -p

+ please input your passwd:

## 创建数据库

+ ```mysql
  create {database|schema}[if not exits]db_name [default]character set{=}charset_name
  ```

## 修改数据库

+ ```mysql
  alter {database|schema}[db_name][default]character set[=]charset_name
  ```

## 创建数据表

```mysql
create table [if not exits] 'runoob_tb1'
(
    'runoob_id' int unsigned auto_increment,
   'runoob_title' varchar(100) not null,
    'runoob_author' varchar(40) not null,
   'submission_date' date,
    primary key('runoob_id)
)ENGINE = InnoDB DEFAULT CHARSET = UTF8;
```

##  drop删除数据库和数据表

+ `drop database database_name`
+ `drop table if exists table_name`

## delete删除表中的记录

+ `del`ete from table_name`
      where clause`

**注：**

​	如果**没有指定**where子句，将会**删除整个表**
​	可以在**where子句**中指定任何条件

## update修改表中的数据

+ update table_name
      set field1 = new-value1,field2 = new-value2
      where clause

+ update table_name
          set field = replace(field,'old string','new string')
          where clause

## alter修改表或者字段的属性

当我们需要修改表名或者修改数据表字段时，就需要使用到mysql **alter命令**

+ **删除，添加或者修改表字段**
+ **alter table table_name drop column_name**
    + 若数据表只剩下一个字段则无法使用drop来删除字段
  +  **alter table table_name add i int;**
    + 执行以上命令后，i字段会自动添加到表字段的末尾
  + **alter table table_name alter i set default 1000**
    + 修改字段的默认值        
    + 将i字段的默认值修改为1000
  
+ **alter table table_name alter i drop default;**
    + 将字段i的默认值删除
  
  + **alter table table_name rename to othername**
  + 修改表名
    + 可以修改表的名字为othername

## SELECT查询

```mysql
select column_name,column_name
    from table_name
    where clause
    limit N offset M
```

查询语句中你可以使用一个或者多个表，表与表之间使用逗号进行分割，并且使用**where语句进行过滤信息**

select命令可以读取一条或者多条记录
可以使用***号代替任意字段**，这样返回的是所有字段的数据
可以使用**where语句包含任何条件**
可以使用**Limit属性来设定返回的记录数**

## group by 分组

```mysql
select column_name,function(column_name)
    from table_name
    where column_name operator value
    group by column_name
```

**group by**语句根据一个或多个列对结果集进行分组
在分组的列上我们可以使用**count sum avg**等函数

## like语句

```mysql
select field1,field2....
    from table_name
    where field1 like condition1 and | or field2 = 'somevalue'
```

+ ‘%a’  以a结尾的数据
+ ‘a%’  以a开头的数据
+ '%a%'  含有a的数据
+ '_a_'   前后两个_，三位中间含有a
+ _ 代表单个字符
+ % 代表0个或者多个字符
+ []  表示括号中所列的任何一个字符

## sort 排序

```mysql
select field1,field2...fieldn
    from table_name1,table_name2...
    order by field1 asc|desc(默认的是asc)           #默认的是升序排列
```

+ 可以使用asc或者desc关键字来设置查询结果是按照升序排列还是降序排列。**默认是升序**

## insert 插入数据

```mysql
insert into table_name
    values(value1,value2...)
```

**不指定列名的时候，默认的是向所有的字段都插入数值**
**如果指定的话，是向指定的字段中插入数值**

```mysql
INSERT INTO `employee_tbl` VALUES ('1', '小明', '2016-04-22 15:25:33', '1'), 
('2', '小王', '2016-04-20 15:25:47', '3'), 
('3', '小丽', '2016-04-19 15:26:02', '2'), 
('4', '小王', '2016-04-07 15:26:14', '4'), 
('5', '小明', '2016-04-11 15:26:40', '4'), 
('6', '小明', '2016-04-04 15:26:54', '2');
```

**可以一次插入多个记录**



## 数据类型

+ 数值类型
  + int
  + tinyint
  + smallint
  + float
  + double
  + decimal

+ 日期和时间类型

  + date
    +  YYYY-MM-DD

  +  time
    + HH:MM:SS

  + year
    + YYYy

  + datetime
    + YYYY-MM-DD HH:MM:SS
  + 字符串类型
            char
                定长字符串
            varchar
                变长字符串
            text
                长文本数据

一个汉字占多少长度与编码有关
    UTF-8:一个汉字 = 3个字节
    GBK:一个汉字 = 2个字节
varchar(n)表示n个字符，无论是汉字和英文，Mysql都可以存入n个字符，仅是实际字节长度有所区别



## 事务

**事务处理可以用来维护数据库的完整性，保证成批的SQL语句要么全部执行，要么全部不执行**
事务用来管理**insert、update、delete**语句

在mysql中，事务都是自动提交的，即执行sql语句后会，马上执行**commit操作**。因此需要显式的开启一个事务
必须使用命令**begin或start transaction,或者执行命令set autocommit = 0,**用来禁止使用当前会话的自动提交。

事务控制语句
    **begin**或者start transaction显式的开启一个事务
    **commit**也可以使用commit work,不过二者是等价的.commit会提交事务，并使对于数据库的操作成为永久性的
    **rollback** 也可以使用rollback work，不过二者是等价的。**回滚会结束用户的事务，并撤销正在进行的所有未提交的修改**

注：
    在mysql中。只有使用了**innodb**数据库引擎的数据库或者表才支持事务
    mysql处理事务哟两种方法
    用begin rollback commit来实现
        **begin 开始一个事务**
        **rollback 事务回滚s**
        **commit事务确认**

