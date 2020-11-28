## 基础指令

+ `创建数据库`

  + CREATE DATABASE 数据库名;
  + CREATE DATABASE IF NOT EXISTS Test DEFAULT CHARSET utf8;

+ `登录数据库`

  + mysql -u root -p pwd

+ `删除数据库`

  + DROP DATABASE 数据库名;

+ `选择数据库`

  + USE 数据库名;

+ `注释`

  + #开头
  + /**/包裹

  

## 检索数据

### SELECT语句

+ 功能
  + 从`一个或者多个表`中检索信息
+ 关键字
  + 作为SQL组成部分的`保留字`。不能用作表或者列名字。
+ 组成
  + 选择什么
  + 哪里选择

> + 结束语句，最好以；结尾
> + SQL语句不区分大小写，关键字最好全部大小，列名和表名小写，便于阅读
> + SQL语句处理的时候，忽略空格。
> + SELECT * FROM table;做好不要这么使用，除非检索所有的列，性能极差。

+ 检索**不同**的值
  + SELECT **DISTINCT** col FROM table;
  + **不能部分使用DISTINCT关键字，该关键字作用的是所有的列。**
+ 限制数值长度
  + SELECT col FROM table **LIMIT** num;
+ 指定开始位置
  + SELECT col FROM table LIMIT num **OFFSET** num;
  + 表示从第num行开始取num行数据。
  + 第一个被检索出来的行是**第0行**。

## 排序检索数据

+ SELECT prod_name FROM products **ORDER BY** prod_name;
  + ORDER BY子句应该在**语句的最后**，否则会报错。
  + 通常情况下，ORDER BY使用的是显示的列，实际上并不一定要这样，用非检索的列排序也是完全合法的。

使用**多个列**进行排序

+ SELECT prod_id, prod_price, prod_name

  FROM products

  ORDER BY prod_price, prod_name;

指定排序方向

​	**默认是升序**，如果想要指定降序，需要加上ASC关键字。

+ **DESC**
  + 降序
+ **ASC**
  + 升序

## 过滤数据

> 使用WHERE子句进行过滤。

WHERE子句位置

+ 同时使用ORDER BY和WHERE子句时，应该让ORDER BY位于WHERE之后，否则将会出错。(ORDER BY子句放在最后就完事儿了)。

WHERE子句还可以结合其他运算符，比如> < >= <=。。。

**不匹配检查**

+ ！=
+ <>

一般情况下，两者可以互换，还是需要根据DBMS文档再做决定。

**范围值检查**

**BETWEEN**关键字，用来限定范围。必须和AND进行联用。

+ **BETWEEN 5 AND 10**

**空值检查**

WHERE col **IS NULL**

## 高级数据过滤

### 多个子句结合

使用逻辑运算符 **AND** **OR** **NOT**进行连接。当使用多个逻辑运算符时，最好加上**括号**进行组合，这样逻辑表达的更加清晰。

### IN操作符

IN操作符完成了OR的功能。

优点

+ IN操作符语法更清楚
+ IN操作符求值顺序更容易管理
+ 操作速度比OR要快