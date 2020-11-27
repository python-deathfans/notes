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