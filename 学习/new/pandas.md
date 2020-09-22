## 整理

+ loc与iloc的区别

  + loc根据的是`索引`
  + iloc根据的是`位置`

+ 排列和随机采样

  + ![](https://pic.downk.cc/item/5f597acb160a154a67840f86.png)

  ![](https://pic.downk.cc/item/5f597b4d160a154a67843e29.png)

+ **合并数据集**
  
  + `pd.merge`
    + 根据一个或多个键将不同DataFrame中的行连接起来
    + 类似于数据库中的join操作
  + `pd.concat`
    + 沿着一条轴将多个对象堆叠到一起
    + axis=0
    + axis=1
  
+ **字符串分割**

  + str.split(str="", num=string.count(str))
  + num
    + 默认是**-1,**表示分割所有
    + 如果传入数值，分割为**num+1**个子串

# excel操作

## 读取操作

+ pd.read_excel()
  + **sheet_name** 用来指定读取的sheet
  + **header**用来指定列索引，默认是0，第一行
  + **index_col**用来指定行索引，默认是1，第一列
  + **usecols**用来指定导入多少列
+ pd.read_csv()
  + **nrows**
    + 指定读入的行数
    + 用于数据较大的时候
+ pd.read_table()
  + 可以用来导入**txt**文件或者**csv**文件
    + txt文件是空格进行分割
    + csv文件是逗号分割文件

## 数据预处理

### 缺失数据

+ `查看缺失值`
  + info()
  + isnull()
+ `删除缺失值`
  + dropna()
    + how='all'
      + 全部是空值的行删除
+ `填充缺失值`
  + 一般缺失数据不超过30%尽量别删除，填充即可
  + fillna()
    + 传入字典，即可进行相应的填充

### 重复数据

+ duplicates()
+ drop_duplicates()
  + subset 指定某些列进行相应的删除重复数据
  + keep='first' or 'last'

### 异常数据

异常值就是**相比正常数据**而言**过高或过低**的数据，比如一个人的年龄是0岁或者300岁都算是一个异常值，因为这和实际情况差距过大。

+ 异常值的显示
  + 根据业务经验划定不同指标的正常范围，超过该范围的值算作异常值。
  + 通过绘制**箱形图**，把大于（小于）箱形图上边缘（下边缘）的点称为异常值。
  + 如果数据服从**正态分布**，则可以利用**3σ 原则**；如果一个数值与平均值之间的偏差超过3倍标准差，那么我们就认为这个值是异常值。
+ 处理方式
  + 最常用的处理方式就是**删除**
  + 把异常值当作缺失值来**填充**。
  + 把异常值当作特殊情况，**研究异常值出现的原因**。
  + 数据替换
    + **replace()**

**箱形图**可以查看异常值

```python
#如何删除异常值
#删除异常值使用函数
def f(data,col):
    q1 = data[col].quantile(q = 0.25)
    q3 = data[col].quantile(q = 0.75)
    iqr = q3 - q1
    t1 = q1 - 3*iqr
    t2 = q3 + 3*iqr
    return data[(data[col]>t1)&(data[col]<t2)][[col]]

#使用方法
df_1 = f(df_1,'col_1')
```



### 数据类型转换

+ 数据分类
  + int
  + float
  + object
  + string_
  + unicode_
  + datetime64
+ 查看
  + **info()**
+ 实现
  + **astype()**

### 索引设置

+ df.columns
+ **set_index**
  + 重新设置索引
+ **rename**
  + 重命名索引
+ **reset_index**
  + drop
    + 是否删除原索引
  + inplace
    + 是否修改原数据

## 数值操作

### 数值替换

数值替换就是将数值A替换成B，可以用在**异常值替换处理**、**缺失值填充处理**中。主要有一对一替换、多对一替换、多对多替换三种替换方法。

+ replace(A, B)
  + 将A替换成B
+ replace([a, b, c], d)
  + 将a, b, c替换为d
+ 多对多进行替换，传入**字典**，即可进行相应的替换

### 数值排序

+ 不含缺失值
  + df.sort_values()
+ **含有缺失值**
  + df.sort_values(na_position='first')

### 数值计数

+ **value_counts**()
  + 针对的是series数据
  + **normalize**
    + 是否显示百分比
  + **sort**
    + 是否排序

### 唯一值获取 

+ unique()

### 数值查找

+ isin()
  + 返回结果是一个Series

### 区间切分

+ pd.cut()
  + bins
  + labels

### 插入新的行或者列

+ insert
+ append

### apply和applymap函数

apply函数主要用于对DataFrame中的**某一column或row**中的元素执行相同的函数操作。

applymap是对于df中的**每个元素**进行相应的操作

## 数据运算

### 汇总计算

+ count()
  + 返回每列的非空值
+ sum()
  + 返回每一列的和
  + axis用来指定是行还是列
+ mean()
+ max()
+ min()

## 时间序列

+ datetime模块

## 数据分组/数据透视表

+ groupby
+ agg

### 数据透视表

> 数据透视表实现的功能与数据分组相类似但又不同，**数据分组**是在**一维（行）方向**上不断拆分，而**数据透视表**是在**行、列**方向上同时拆分。

