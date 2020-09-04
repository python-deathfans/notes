# 总结

## value_counts()

+ Series()类型的函数
+ 按照某种规则统计词频出现的次数
+ 默认是`index`
+ `ascending`参数
+ `normalize`参数
  + 是否计算百分比
+ dropna参数
  + 默认是True, 删除na值
  + `dropna=False,此方法可以统计na值`

## to_list()

+ `series.values.to_list()`
+ 将series数据转换成列表

## 缺失值处理

### dropna()

+ 对于series数据，会删除对应的数据
+ 对于dataframe数据，会删除对应的`行`
+ `how`
  + 如何删除
  + all    所有都为na的时候才会删除行
+ `axis`
  + 0，表示行
  + 1， 表示列
+ `thresh`
  + 代表删除之后还剩下的数量
+ `subset`
  + 传入一个list,代表删除list中的含有空值的行

### fillna()

+ value
  + 全部填充为value
+ `传入字典`
  + 为不同的列传入不同的数值
+ `method`
  + ffill
  + bfill
+ 还可以使用统计数据进行填充

### 删除重复值

原始数据中有大量重复的行，需要我们删除，让数据更健康

+ `df.duplicated()`
  + `此行的数据是否在前面出现过`
  + 也可以对于`某一列`进行删除重复的数据
+ df.drop_duplicates()
  + 删除重复的数据

### 替换值

`df.replace()`

+ 单个值， 单一替换
+ 传入列表，集体替换
+ 传入字典，逐一替换

## pd.cut()

+ 将数据进行`离散化`
+ pandas.**cut**(x,bins,right=True,labels=None,retbins=False,precision=3,include_lowest=False)
  + `x`:进行划分的一维数组
  + `bins`:1, 整数--将x划分为`多少个等间距`的区间
  + `right`:是否包含右端点
  + `labels`:对应区间的标签

## Series中的map函数

+ 接收一个`函数`或者含有映射关系的`字典对象`

GroupBy函数

+ `size函数`
  + 返回一个Series对象
  + index是聚合的结果
  + value是每个index对应的值

## pd.merge()

> pd.merge(left, right, how='inner', on=None, left_on=None, right_on=None,         left_index=False, right_index=False, sort=True,         suffixes=('_x', '_y'), copy=True, indicator=False,         validate=None)

+ left
  + 左侧拼接对象
+ right
  + 右侧拼接对象
+ `on`
  + 要加入的列或索引级别名称
  + 必须在左侧和右侧DataFrame对象中找到
+ `how`
  + One of ‘`left`’, ‘`right`’, ‘`outer`’, ‘`inner`’. 默认inner。`inner是取交集`，`outer取并集`。比如left：[‘A’,‘B’,‘C’];right[’'A,‘C’,‘D’]；inner取交集的话，left中出现的A会和right中出现的买一个A进行匹配拼接，如果没有是B，在right中没有匹配到，则会丢失。'outer’取并集，出现的A会进行一一匹配，没有同时出现的会将缺失的部分添加缺失值。

## pd.melt()

> 数据分析的时候经常要把`宽数据--->>长数据`，有点像你们用excel 做透视跟逆透视的过程
>
> pandas.melt(frame,id_vars=None,value_vars=None,var_name=None,value_name='value',    col_level=None)

+ `frame`
  + 需要处理的数据集
+ `id_vars`
  + 不需要转换的列名
+ `value_vars`
  + 需要转换的列名，如果剩下的列全部都要转换，就不用写了
+ `var_name`和`value_name`是自定义设置对应的列名

## df.nunique()

+ 统计某个Series中`不重复的个数`

## 修改列名

+ df.`rename`(columns={'oldname': 'newname'}, inplace=True)

## 添加一行数据

+ df.`append`(data, ignore_index=True)

## 合并数据

+ df.`concat`([data1, data2], axis=0, ignore_index=True)
  + 按照行进行合并
  + 不考虑数据的索引

## agg函数

DataFrame.agg（func，axis = 0,*args, **kwargs）

+ func
  + 函数，函数名称，`函数列表`，`字典`
+ 使用指定轴上的一个或者多个操作进行聚合

## 数据交换

```python
cols = df.columns[[0,2,1,3,4,5,6]]
df1 = df[cols]
df1
```

## 数据拆分

```python
# expand=True, 将结果转换成DataFrame,并且索引和原来的df一样，可以使用pd.merge进行合并
df['技能要求'].str.split(',',expand=True)
```

## 数据抽样

```python
df.sample(20)
```

