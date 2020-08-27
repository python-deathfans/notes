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

+ 将数据进行离散化
+ pandas.**cut**(x,bins,right=True,labels=None,retbins=False,precision=3,include_lowest=False)
  + `x`:进行划分的一维数组
  + `bins`:1, 整数--将x划分为`多少个等间距`的区间
  + `right`:是否包含右端点

## jieba 词云



