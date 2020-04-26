# 1 基础知识

+ 表
  + 一种特定类型的**结构化**清单
  + 相同数据库不能两次使用相同的表名，但是不同的数据库可以使用相同的表名
+ **模式(schema)**
  + 关于数据库和表的布局及特性的信息
  + 用来描述数据库中的表，也可以描述整个数据库
+ **主键**
  + 一列(或多列)，其值可以**唯一表示表中每一行**
    + 任意两行不具有相同的主键值
    + 每一行的主键值**不能为NULL**
    + 主键列中的值**不允许修改和更新**
+ **注：**
  + 存储在表中的数据是**同一种类型**的数据或清单，不应该将**顾客清单**与**订单清单**放置在一个表中
  + 表中的数据是**按行存储**的，所保存的每个记录存储在自己的行内。如果将表想象为网格，网格中垂直的列为表列，水平行为表行。

# 2 检索数据

+ **提示**
  
  + 多条语句必须以；分隔
  + SQL语句不区分大小写，因此SELECT和select相同
  + 在处理SQL语句时，所有空格都被忽略
  + **DISTINCT** 关键字作用于**所有的列**，不仅仅是跟在其后的那一列。
  + **DISTINCT**关键字会返回独有的值，**关键字放在字段前面**
  + **LIMIT** 关键字用来限制返回的记录数，**mysql**的用法，放在最后。
    + 配合**OFFSET**关键字可以更加细致的限定返回结果。
    + 注第一个检索的是**第0行**
    + 简写为LIMIT 3, 4；
      + 从第3行开始的4行数据
  
+ 注释

  + **单行注释**
    + #
    + --

  + **多行注释**
    + /*sdfsa*/

# 3 排序检索数据

+ **注：**
  + 在指定一条 **ORDER BY** 子句时，应该保证它是 SELECT 语句中**最后一条子句**。如果它不是最后的子句，将会出现错误消息。可以使用**列名进行排序**，也可以使用**相对位置排序**。
  + **DESC**
    + 降序
  + **ASC**
    + 升序(默认)

# 4 过滤数据

+ ![](https://pic.downk.cc/item/5e8c2119504f4bcb04e5d00a.png)
+ 注：
  + 在同时使用 ORDER BY 和 WHERE 子句时，应该让 **ORDER BY 位于WHERE 之后**，否则将会产生错误
+ 不匹配检查
  + != 和 <> 通常可以互换。但是，并非所有 DBMS都支持这两种不等于操作符。
+ 范围值检查
  + between and

# 5 高级数据过滤

+ **and**用在where子句中的关键字，用来指示检索满足所有给定条件的行

+ **or**同理

+ 任何时候使用具有 **AND** 和 **OR** 操作符的 WHERE 子句，都应该使用**圆括号**明确地分组操作符。不要过分依赖默认求值顺序，即使它确实如你希望的那样。

+ in操作运算符

  + ```sql
    SELECT prod_name, prod_price
    FROM Products
    WHERE vend_id IN ( 'DLL01', 'BRS01' )
    ORDER BY prod_name;
    ```

+ **not**操作运算符
  
  + 不匹配后面的内容

# 6 用通配符进行过滤

+ **like**操作符
  + **%** 表示**任何字符出现任意次数**
  + **_** 表示单个字符
  + **[]** 用来指定一个字符集
  + **^** 用来表示否定

# 7 创建计算字段

+ 概念
  + 计算字段
  + **拼接**字段
    + 将值联结到一起构成单个值
    + +可以拼接字符
    + **mysql** 使用**concat**函数进行拼接

## 8 汇总数据

+ 聚集函数(aggregate function)
  + 定义
    + 对**某些行**运行的函数，计算并返回一个值
  + 分类
    + AVG
    + COUNT
      + 如果是COUNT(*)， 不忽略列值为NULL的行
      + 如果是传入的具体的列，自动忽略NULL的行
    + MAX
    + MIN
    + SUM

# 9 分组数据

+ GROUP BY
  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-05_09-56-22.png" style="zoom:80%;" align='center'/>
+ HAVING
  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-05_09-58-37.png" style="zoom:80%;" />

+ order by
  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-05_10-01-15.png" style="zoom:80%;" />

+ **select子句顺序**
  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-05_10-02-00.png" style="zoom:80%;" />

# 10 联结表

+ 关系表的设计就是要把**信息分解成多个表**，**一类数据一个表**。各表通过某些**共同的值**互相关联（所以才叫**关系数据库**）。
+ 将数据分解为多个表能更有效的存储，更方便的处理，并且**伸缩性**更好
+ 如果数据存储在多个表中，怎样用一条SELECT语句就检索出来？答案是**联结**

  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-05_10-09-09.png" style="zoom:80%;" />

  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-05_10-11-30.png" style="zoom:80%;" />
+ **内连接**，也叫**等值联结**，基于两个表之间**相等测试**
+ 多表联合
  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-05_10-13-47.png" style="zoom:80%;" />

## 11 创建高级联结

+ 联结分类
  + 自联结(**self-join**)
    + ![](https://pic.downk.cc/item/5e8d38e0504f4bcb04d137ab.png)
  + 内连接(**inner join**)
    + 可以自定义两张表的不同列字段
  + 自然联结(**natural join**)
    + **不用指定连接列**，也**不能使用ON语句**，默认比较两个表中**相同的列**
  + 外联结(**outer join**)
    + 联结包含了那些在相关表中**没有关联行**的行.
    + 分类
      + 左外连接
        + 返回指定**左表的全部行**+**右表对应的行**，如果左表中数据在右表中没有与其相匹配的行，则在查询结果集中显示为**空值**。
      + 右外连接
        + 返回指定**右表的全部行**+**左表对应的行**，如果右表中数据在左表中没有与其相匹配的行，则在查询结果集中显示为**空值**。

## 12 组合查询

+ **UNION**关键字
+ 使用场景：
  - [ ] 在一个查询中从**不同的表**返回结构数据；
  - [ ] 对一个表执行**多个查询**，按一个查询返回数据。

+ ![](https://pic.downk.cc/item/5e8d3d11504f4bcb04d4a963.png)

+ UNION规则
  - [ ] UNION 必须由**两条或两条以上**的 SELECT 语句组成，语句之间用关键
    字 UNION 分隔（因此，如果组合四条 SELECT 语句，将要使用三个 UNION
    关键字）。
  - [ ] UNION 中的每个查询必须包含**相同的列**、**表达式**或**聚集函数**（不过，
    各个列不需要以相同的次序列出）。
  - [ ] 列数据类型必须兼容：类型不必完全相同，但必须是 DBMS可以隐含
    转换的类型（例如，不同的数值类型或不同的日期类型）

# 13 插入数据

+ **INSERT SELECT**

  + 插入数据
  + 将数据添加到一个已经存在的表
  
+ **SELECT INTO**

  + 将数据复制到一个新表
  
  + ```sql
    SELECT *
    INTO CustCopy
    FROM Customers;
    ```
  ```
  
  + mysql中
  
    + ```mysql
      CREATE TABLE CUSTCOPY AS
      SELECT * FROM Customers;
  ```
  
  ​    
  
+ 复制表

  + ```python
    SELECT prod_name, prod_price
    FROM Products
    WHERE vend_id IN ( 'DLL01', 'BRS01' )
    ORDER BY prod_name;
    ```

  + ```sql
    SELECT prod_name, prod_price
    FROM Products
    WHERE vend_id IN ( 'DLL01', 'BRS01' )
    ORDER BY prod_name;
    ```

    

# 14 使用视图

+ 视图是**虚拟**的表

+ 与包含数据的表不一样，视图只包含使用时**动态检索数据**的查询。

+ 作为视图，不包含任何列或者数据，包含的是一个查询

+ 创建视图

  + ```sql
    CREATE VIEW ProductCustomers AS
    SELECT cust_name, cust_contact, prod_id
    FROM Customers, Orders, OrderItems
    WHERE Customers.cust_id = Orders.cust_id
    AND OrderItems.order_num = Orders.order_num;
    ```

# 15 使用存储过程

+ 什么是存储过程
  + **为以后使用而保存的一条或多条SQL语句**，可将其视为批文件，虽然它们的作用不限于批处理
+ 为什么需要存储过程
  + 通过把处理封装在一个易用单元中，可以简化复杂的操作
  + 简化对变动的管理
  + 由于存储过程通常以编译过的形式存储，所以DBMS处理命令所需工作量少

# 16 管理事务处理

+ 事务处理

  + 使用事务处理（transaction processing），通过确保成批的 SQL 操作**要么完全执行**，**要么完全不执行**，来维护数据库的完整性。
  + 术语：
    + 事务：指的是一组SQL语句
    + 回退：撤销指定SQL语句的过程
    + 提交：将没有存储的SQL语句结果写入数据库表
    + 保留点：事务处理中设置临时占位符(placeholder)，可以对它发布回退

+ 控制事务管理

  + rollback

    + ```sql
      DELETE FROM ORDERS;
      ROLLBACK
      ```

  + COMMIT

    + **一般**的 SQL语句都是针对数据库表**直接执行和编写**的。这就是所谓的**隐式提交**（implicit commit），即提交（写或保存）操作是自动进行的。在**事务处理**块中，提交不会隐式进行。

    + ```sql
      BEGIN TRANSACTION
      DELETE OrderItems WHERE order_num = 12345
      DELETE Orders WHERE order_num = 12345
      COMMIT TRANSACTION
      ```

# 17 使用游标

+ 游标(cursor)
  + 一个存储在 DBMS 服务器上的**数据库查询**，它不是一条 SELECT 语句，而是被该语句检索出来的**结果集**。

# 18 高级SQL特性

+ 约束

  + 管理如何插入或处理数据库数据的规则

  + 主键

    + ```sql
      ALTER TABLE VENDORS
      ADD CONSTRAINT PRIMARY KEY (vend_id)
      ```

  + 外键
    + 是表中的一列
    + 必须为另一个表中的主键
    + 是保证引用完整性的及其重要部分
    + ![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-05_11-27-54.png)
    + ![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-05_11-28-39.png)
  + 唯一约束
    + 类似于主键，但是还是有区别
    + 和主键的区别
      + 表可包含多个唯一约束，但每个表只允许一个主键。
      + 唯一约束列可包含 NULL 值。
      + 唯一约束列可修改或更新。
      + 唯一约束列的值可重复使用。
      + 与主键不一样，唯一约束不能用来定义外键
  + 检查约束

+ 索引

  + 索引用来**排序数据**以加快搜索和排序操作的速度

  + 注

    + 索引改善检索操作的性能，但降低了数据插入、修改和删除的性能。在执行这些操作时，DBMS必须动态地更新索引。
    + 索引数据可能占据大量的存储空间
    + 并非所有数据都适合做索引。
    + 索引用于**数据过滤和排序**
    + 可以在索引中定义多个列

  + 定义

    + ```sql
      CREATE INDEX prod_name_id
      ON Products (prod_name);
      ```

    + 索引必须唯一命名

+ 触发器

