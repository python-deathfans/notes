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

### 用通配符进行过滤

> + 不要过度使用通配符，检索效率比较低

+ **LIKE**操作符
  + **%** 
    + **任何字符出现任何次数**
    + SELECT prod_id, prod_name FROM products WHERE prod_name LIKE 'F%'
    + ACCESS中使用的是*
  + **_**
    + 匹配**单个字符**
  + **[]**
    + 用来**指定一个字符集**，必须匹配指定位置的一个字符
  + **^**
    + 用来表示**否定**
    + 也可以使用**NOT**关键字表示否定。

### 创建计算字段

+ 拼接字段
  + **+**进行拼接多个字段
+ 使用别名
  + **AS**关键字
+ 执行运算
  + SELECT 2*3;
  + SELECT NOW();
  + SELECT TRIM('abc');

------



## 汇总数据

### 聚集函数

- AVG()
  - ![](https://pic.downk.cc/item/5fc9d8ba394ac52378ff7aa1.png)
- COUNT()
  - 确定表中行的数目或符合特定条件的列的数目
  - 两种用法
    - COUNT(*)
      - 对表中的所有行进行计数，**不管行中包含的是NULL还是非NULL**
    - COUNT(COLUMN)
      - 对特定列中具有值的行进行计数，**忽略NULL值**
- MAX()
- MIN()
- SUM()

对**某些行**运行的函数，计算并返回一个值。

## 分组数据

涉及两个新SELECT 语句子句：

+ GROUP BY
+ HAVING子句

### 创建分组

分组是使用SELECT语句的GROUP BY子句创建的。

![](https://pic.downk.cc/item/5fc9db8f394ac52378020ef2.png)

### 过滤分组

HAVING 非常类似于WHERE子句。唯一的差别是WHERE过滤行，HAVING过滤分组。

![](https://pic.downk.cc/item/5fc9ddce394ac523780553f7.png)



### 分组和排序

ORDER BY子句放在SQL语句最后。

### SELECT 子句顺序

SELECT	要返回的列或者表达式

FROM	检索的表

WHERE	行级过滤

GROUP BY	分组说明

HAVING	分组过滤

ORDER BY	输出排序顺序

## 使用子查询

子查询

+ 嵌套在其他查询中的查询
+ ![](https://pic.downk.cc/item/5fc9e390394ac523780a6ed1.png)

+ 子查询总是子内向外

## 联结表

联结(**join**)表。

联结是SQL中一个**最重要、最强大的特性**，有效地使用联结需要对关系数据库设计有基本的了解。

关系表的设计就是要把信息分解成多个表，一类数据一个表。各表通过某些共同的值相互关联，所以才叫关系型数据库。

![](https://pic.downk.cc/item/5fcb2465394ac52378340605.png)

如果没有**WHERE语句**，则进行的是**笛卡儿积**，最后的结果是两张表的行数之积。

### 内联结

inner join。

SELECT vend_name, prod_name, prod_price FROM vendors INNER **JOIN** products

**ON** vendors.vend_id=products.vend_id

+ 这里，两个表之间的关系是以**INNER JOIN**指定的部分FROM子句。在使用这种语法时，联结条件用特定的**ON**子句而不是WHERE子句给出。

联结的时候可以使用多种语法，一种是**SELECT FROM WHERE**,另一种是**SELECT FROM JOIN ON**。。。