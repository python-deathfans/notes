[TOC]



## 新建登陆账号

+ windows登陆验证
  	不需要配置，可以直接使用，但是可移植性不好，只能在win平台上使用
+ sql server登陆验证
  	**1、先以windows登陆验证，进入软件**
    	**2、点击安全性**
    	**3、新建登陆账号**
    	**4、选择sql server登陆验证,设置用户名和密码**
    	**5、退出软件，重新登陆即可**



## 附加和分离数据库

+ 分离数据库
  	1、右击数据库
    	2、点击任务
    	3、点击分离

+ 附加数据库
  	1、右击数据库
    	2、点击附加
    	3、选择数据文件(mdf文件)



## 查询

```mysql
select * from emp;		
select ename,sal from emp;
select ename,sal * 12 as "年薪"from emp;	// as 可以省略，记住年薪需要带双引号
select 5 from emp;	// 输出的行数是emp表的行数 每行只有一个字段
```

​		select ename,sal * 12  as  "年薪",from emp;	// **as 可以省略，记住年薪需要带双引号**
​		select 5 from emp;	// 输出的行数是emp表的行数 每行只有一个字段
​		select **distinct** deptno from emp;	//**输出不重复的deptno的字段**
​		select ename as "姓名" from emp;	//**取个别名**

+ **between**
  		select * from emp
    			**where sal >= 1500 and sal <= 3000**
    		等价于
    			select * from emp
    				**where sal between 1500 and 3000**
+ **in**
  		属于若干个孤立的值
    		select * from emp where sal **in** (1500,3000,5000)
    		select * from emp where sal **not in** (1500,3000,5000)
    		等价于
    		select * from emp where sal = 1500 or sal = 3000 or sal = 5000
    		select * from emp where sal = 1500 or sal = 3000 or sal = 5000
+ **top**
  		select **top 2** * from  emp
    		select **top 15 percent** * from emp
+ **null**
  		**is null**
    		**is not null**
    		其他运算都是错误的
+ **order by**
  		升序还是降序
    		**order by sal desc(降序)**
    		**不写的话，默认是升序**
+ 模糊查询
  		select *
    			from emp
    			where ename like '%A%'
  + 通配符
    			%  表示任意**零个或者多个**字符
          			-	表示任意的**单个字符**
       
              			[a-f]	**a-f中的任意单个字符**
              			[a,f]	**a或者f**
            			[~a-c]	**~表示取反的意思**
  
+ 聚合函数
  		单行函数
    			每行返回一个值
    		多行函数
    			多行返回一个值
    		**max**
    		**min**
    		**avg(平均值)**
    		**count(字段名)**
    			返回表中所有记录的个数
    		**count(distinct 字段名)**
    			返回表中不重复记录的个数
  + group by
    		分组
      		按照某个字段进行分组
      		**选取的字段必须是分组之后的内容，不能是所有的内容**
      	**having**
      		**分组之后的信息进行过滤**
      		因此要使用having,通常来说先试用group by
      		只可以用原始的字符，不能用别名
  
+ 连接查询
  + 定义
    + 将两个表或者多个表以一定的条件进行连接起来
      		从中检索出满足条件的数据
        	分类
        		内连接
        			1、**select ... from A,B 的用法**
        				**产生的结果是:行数是 A*B 列数是 A+B**
        			2、**select ... from A,B where ... 的用法**
        				**过滤一下信息**
        			3、**select ... from A join B on ...的用法**
        				**join 和 on 必须同时出现，on后面表示的是连接的条件**
        				**一般来说,on中只写连接条件，where中写过滤条件，二者需要分开写**
        			4、select ... from A,B where  sql 92标准
        				select ... from A join B on...	sql 99标准（推荐）
        			5、select、from where join on group order



## add constraint

+ -- 添加主键约束
  	alter table 表名
    	add constraint 约束名 primary key(主键字段)

+ -- 添加唯一约束
  	alter table 表名
    	add constraint 约束名 unique(字段)

+ -- 添加外键约束
  	alter table 表名
    	add constraint 约束名 foreign key (关联字段) references 主表(关联字段)



## 增删查改

+ **插入表数据**
  	**insert into table_name values()		# 没有指定列名**
    	**insert into table_name(column1,column2) values(value1,value2)	# 指定列名**
  *建表时复制原表中的数据*
  	**create table table_name as select * from table_name2**

+ **修改表数据**
  	**update语句**
    **无条件更新**
    			update table_name set userpwd = '324',email = '32442432'
    		有条件更新
    			update table_name set 
    				where condition
    			update top(4) SPJ set QTY = 300

  ​			修改前四行的QTY字段值为300

+ **删除表**
  	无条件删除
    		**delete from table_name**
    	有条件删除
    		**delete from table_name where condition**

+ **给表添加一个字段**
  	**alter table 表名 add 字段 type**
    		当type = date时不需要加长度

+ **改变字段的属性值**
  	alter table 表名 alter column 字段 type



## 视图

**可视化的表**
是基于sql语句的结果集的可视化的表

```mysql
create view view_name as
select column_name
from table_name
where condition
```


## 关于时间的函数

+ 根据出生日期计算年龄
  	**FLOOR(datediff(DY,birthday,getdate())/365.25)**

+ **getdate** 返回当前的日期和时间、
+ **datepart** 返回日期/时间的单独部分
+ **dateadd** 在日期中添加或者减去指定的时间间隔
+ **datediff** 返回两个日期之间的时间
+ **convert** 用不同的格式显示日期/时间
+ sql server数据库存储日期
  + **date** YYYY-MM-DD
  + **datetime**	YYYY-MM-DD HH:MM:SS



## sql函数

+ sql aggregate(计算从列中取得的值，返回一个单一的值)

  + **avg**		返回平均值
  + **count**	返回行数
    + 当记录的值是**NULL**时，不计入行数之内

  + **first**	返回第一个记录的值
    + select first(column_name) from table_name
    + select top 1 column_name from table_name	order by column_name

  + **last**	返回最后一个记录的值
  + **max**		返回最大的值
  + **min**		返回最小的值
  + **sum**		返回总和

+ **now**
  	返回现在的日期和时间
+ **date_format**
  	日期格式化函数，用于把日期转换成指定的格式
    	date_format(now(),'%Y-%m-%d')



## 触发器

+ 分类
  + **DML触发器**
    		数据操控语言触发器
      		指的是在表或者视图中进行数据的**insert、update、delete**的操作的语句
  + **DDL触发器**
    		数据定义语言触发器
      		在表或索引中的create、alter、drop操作的语句

+ DML触发器触发方式可以分为以下两种：
  + **after触发器**（之后触发）
    + 只有执行insert update delete 某个操作才会被触发，且**只能定义在表中**
  + **instead of 触发器**（之前触发）
    + instead of触发器并不执行其定义的操作，而仅仅执行触发器本身。
    + 可以在**表或者视图**上定义instead of 触发器

+ DML触发器有两种特殊的表（定义触发器的时候就会建立的）：
  + **inserted表**
  + **deleted表**
  + 这两张表都是**逻辑表**，是建立在数据库服务器内存中，而且两张表都是**只读的**

+ after触发器（之后触发）语法:
  	**create trigger trigger_name**
    	**on table_name|view_name**
    	**for|after insert|update|delete**
    	**as**
    	**sql_statement**

![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\图片1.png )



```sql
if(OBJECT_ID('tri_update_delete_stu') is not null)        -- 判断名为 tri_update_delete_stu 的触发器是否存在
drop trigger trigger_Stu_Insert        -- 删除触发器
go

create trigger tri_update_delete_stu
on student
for update,delete
as

if update(课程)
	begin
	select deleted.课程 as "原成绩", inserted.课程 as "新成绩"
		from deleted
		join inserted
		on deleted.stu_id = inserted.stu_id
	
	select * from student
	end
else if columns_updated()=0
	begin
	select * from deleted
	end
else
	print '没有更新成绩'
```

+ 声明局部变量
  + declare @variable_name Data Type

+ 给局部变量赋值
  + set @variable_name = value
  + select @variable_name = value



## Tips

+ ```sql
  if update(column_name)
  	--某个字段更新，会发生什么事情
  ```

+ ```sql
  insert into T1 select * from T2
  	-- 经常用来数据插入 必须事先有表
  ```

+ ```sql
  select * into T1 from T2 
  	-- 大部分用来备份数据
  ```

+ ```sql
  -- 用来表示流程控制
  -- 用来配合if和while
  -- 包含在其中的语句属于同一个流程控制
  ```

+ ```sql
  -- go 用来隔开事务
  -- 每个隔开的是一个事务
  -- 彼此互不影响
  ```

+ ```sql
  -- @ 表示局部变量，用户可以自己定义，使用declare关键字，只能在程序内部使用
  -- @@ 表示全局变量，系统定义，可以在任何地方使用
  ```

+ ```sql
  -- @@rowcount  表示受影响的行数，是全局变量
  ```

+ ```sql
  -- 局部变量赋值方法
  	set @var = value
  	select @var = value
  	select @var = 字段名 from 表名 where....
  ```

  