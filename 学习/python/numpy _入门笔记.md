[TOC]



# 1. Numpy 简易入门 

## 1.1 认识ndarray对象


```python
import numpy as np
```


```python
array = np.array(
        [
            [12, 3, 5],
            [45, 23, 5]
        ]
)
```


```python
array
```




    array([[12,  3,  5],
           [45, 23,  5]])




```python
type(array)
```




    numpy.ndarray




```python
array.dtype
```




    dtype('int32')




```python
array.dtype.name
```




    'int32'




```python
array.ndim
```




    2




```python
array.shape
```




    (2, 3)




```python
array.size
```




    6



## 1.2 创建array数组


```python
a = np.array([2, 34, 5], dtype=np.int32)  # 创建一个一维数组
a
```




    array([ 2, 34,  5])




```python
np.array([
    [2, 34, 5],
    [45, 6, 7]
])    # 创建一个二维数组
```




    array([[ 2, 34,  5],
           [45,  6,  7]])




```python
np.zeros((3, 2))    # 创建一个全零数组
```




    array([[0., 0.],
           [0., 0.],
           [0., 0.]])




```python
np.ones((3, 2))    # 创建一个全一数组
```




    array([[1., 1.],
           [1., 1.],
           [1., 1.]])




```python
np.empty((3, 2))    # 创建全空数组，其实每个值都是接近于0的数
```




    array([[1., 1.],
           [1., 1.],
           [1., 1.]])




```python
np.arange(10, 21, dtype=np.float)
```




    array([10., 11., 12., 13., 14., 15., 16., 17., 18., 19., 20.])




```python
np.linspace(-1, 2, 10)
```




    array([-1.        , -0.66666667, -0.33333333,  0.        ,  0.33333333,
            0.66666667,  1.        ,  1.33333333,  1.66666667,  2.        ])



## 1.3 ndarray对象的数据类型

### 1.3.1 查看数据类型


```python
a = np.array([[12,3,5], [44, 56, 6]])
a.dtype.name
```




    'int32'



### 1.3.2 转换数据类型


```python
float_a = a.astype(np.float32)
float_a
```




    array([[12.,  3.,  5.],
           [44., 56.,  6.]], dtype=float32)



## 1.4 数组的运算


```python
a = np.array([10, 20, 30, 40])
b = np.arange(4)
a-b
```




    array([10, 19, 28, 37])




```python
a+b
```




    array([10, 21, 32, 43])




```python
b**2
```




    array([0, 1, 4, 9], dtype=int32)




```python
a == b
```




    array([False, False, False, False])




```python
a = np.array([[1, 1], [0, 1]])
b = np.arange(4).reshape((2, 2))
print(a)
print(b)
```

    [[1 1]
     [0 1]]
    [[0 1]
     [2 3]]



```python
a.dot(b)                     
```




    array([[2, 4],
           [2, 3]])




```python
a = np.random.random((2, 4))
a
```




    array([[0.78507581, 0.2170868 , 0.27674388, 0.69284854],
           [0.1379581 , 0.23427404, 0.82547609, 0.63917968]])




```python
a.min()
```




    0.1379580973328013




```python
a.max()
```




    0.8254760945649273




```python
a.sum()
```




    3.808642938854845




```python
a
```




    array([[0.78507581, 0.2170868 , 0.27674388, 0.69284854],
           [0.1379581 , 0.23427404, 0.82547609, 0.63917968]])




```python
a.sum(axis=0)  # 对列进行求和
```




    array([0.92303391, 0.45136084, 1.10221997, 1.33202822])




```python
a = np.arange(2, 14).reshape((3, 4))
a
```




    array([[ 2,  3,  4,  5],
           [ 6,  7,  8,  9],
           [10, 11, 12, 13]])




```python
np.argmin(a)  # 最小元素索引
```




    0




```python
np.argmax(a)
```




    11




```python
np.mean(a)
```




    7.5




```python
# 累加
np.cumsum(a)
```




    array([ 2,  5,  9, 14, 20, 27, 35, 44, 54, 65, 77, 90], dtype=int32)




```python
# 累差运算
np.diff(a)
```




    array([[1, 1, 1],
           [1, 1, 1],
           [1, 1, 1]])




```python
a
```




    array([[ 0,  5,  9],
           [ 4,  0, 10]])




```python
# 矩阵转置
np.transpose(a)
```




    array([[ 0,  4],
           [ 5,  0],
           [ 9, 10]])



## 1.5 Numpy索引与切片


```python
a = np.arange(3, 15).reshape((3, 4))
a
```




    array([[ 3,  4,  5,  6],
           [ 7,  8,  9, 10],
           [11, 12, 13, 14]])




```python
a[0]
```




    array([3, 4, 5, 6])




```python
a[0][2]
```




    5




```python
a[0,2]
```




    5




```python
# 切片操作
a[1:, 2:]
```




    array([[ 9, 10],
           [13, 14]])




```python
# 打印行
for row in a:
    print(row)
```

    [3 4 5 6]
    [ 7  8  9 10]
    [11 12 13 14]



```python
# 打印列
for col in a.T:
    print(col)
```

    [ 3  7 11]
    [ 4  8 12]
    [ 5  9 13]
    [ 6 10 14]



```python
# 多维变成一维
a.flatten()
```




    array([ 3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14])



## 1.6 数组合并


```python
a = np.array([1, 1, 1])
b = np.array([2, 2, 2])
# vertical stack
np.vstack((a, b))
```




    array([[1, 1, 1],
           [2, 2, 2]])




```python
# horizontal stack
np.hstack((a, b))
```




    array([1, 1, 1, 2, 2, 2])




```python
a = np.arange(8).reshape(2, 4)
b = np.arange(8).reshape(2, 4)
print(a)
print(b)
```

    [[0 1 2 3]
     [4 5 6 7]]
    [[0 1 2 3]
     [4 5 6 7]]



```python
# 横向合并
c = np.concatenate((a, b), axis=1)
c
```




    array([[0, 1, 2, 3, 0, 1, 2, 3],
           [4, 5, 6, 7, 4, 5, 6, 7]])




```python
# 纵向合并
c = np.concatenate((a, b), axis=0)
c
```




    array([[0, 1, 2, 3],
           [4, 5, 6, 7],
           [0, 1, 2, 3],
           [4, 5, 6, 7]])



## 1.7 添加一个维度


```python
a.T
```




    array([1, 1, 1])




```python
a.shape
```




    (3,)




```python
a[np.newaxis, :].shape
```




    (1, 3)




```python
a[:, np.newaxis].shape
```




    (3, 1)



## 1.8 numpy copy与=


```python
a = np.arange(4)
a
```




    array([0, 1, 2, 3])




```python
# = 赋值方式带有关联性
b = a
c = a
a[0] = 10
print(a)
print(b)
print(c)
```

    [10  1  2  3]
    [10  1  2  3]
    [10  1  2  3]



```python
# copy()方式没有关联性，相当于创建了一个新的变量
b = a.copy()
b[0] = 9
print(b)
print(a)
```

    [9 1 2 3]
    [10  1  2  3]


## 1.9 广播机制

numpy数组间的运算是一对一的，也就是`a.shape==b.shape`，但是两者不同的时候，会自动触发广播机制，如下：


```python
a = np.array([
        [0, 0, 0],
        [10, 10, 10],
        [20, 20, 200]
])
b = np.array([0, 1, 2])
a+b
```




    array([[  0,   1,   2],
           [ 10,  11,  12],
           [ 20,  21, 202]])




```python
a = np.array([
        [1, 2],
        [34, 5]
])
b = np.array([23, 45])
print(a.shape)
print(b.shape)
```

    (2, 2)
    (2,)



```python
a+b
```




    array([[24, 47],
           [57, 50]])



## 1.10 常用函数

### 1.10.1 np.bincount()


```python
x = np.array([1, 2, 4, 6, 4, 2, 1])
# bincount返回的数组的元素的个数比数组中最大数大1，表示的是索引出现的次数
np.bincount(x)
```




    array([0, 2, 2, 0, 2, 0, 1], dtype=int64)



### 1.10.2 np.argmax()


```python
x = np.array([
        [1, 4, 5],
        [7, 43, 7]
])
np.argmax(x)
```




    4




```python
np.argmax(x, axis=1)
```




    array([2, 1], dtype=int64)



### 1.10.3 求取精度


```python
np.around([-0.3, 1.23, 45.54, 54.4, -9.6], decimals=0) # 取指定位置的精度
```




    array([ -0.,   1.,  46.,  54., -10.])



取整


```python
# 负数取整，取绝对值大的
np.floor([-0.6, 12.3, -90.4])
```




    array([ -1.,  12., -91.])



### 1.10.4查找


```python
x = np.array([
        [1, 0],
        [2, -2],
        [-2, 1]
])
x
```




    array([[ 1,  0],
           [ 2, -2],
           [-2,  1]])




```python
"""
第一个参数是条件
满足条件的取 x,
不满足条件的取0

"""
np.where(x>0, x, 0)
```




    array([[1, 0],
           [2, 0],
           [0, 1]])



### 1.10.5 数组排序 


```python
arr = np.array([
        [6, 2, 7],
        [3, 6, 2],
        [4, 3, 2]
])
arr
```




    array([[6, 2, 7],
           [3, 6, 2],
           [4, 3, 2]])




```python
arr.sort()
arr
```




    array([[2, 6, 7],
           [2, 3, 6],
           [2, 3, 4]])



### 1.10.6 检索数组元素


```python
arr = np.array([
        [1, -2, -8],
        [-3, 6, 2],
        [-4, 3, 2]
])
arr
```




    array([[ 1, -2, -8],
           [-3,  6,  2],
           [-4,  3,  2]])




```python
np.any(arr > 0)
```




    True




```python
np.all(arr > 0)
```




    False



### 1.10.7 唯一化及其他集合逻辑


```python
arr = np.array([12, 11, 34, 23, 12, 8])
```


```python
arr
```




    array([12, 11, 34, 23, 12,  8])




```python
np.unique(arr)
```




    array([ 8, 11, 12, 23, 34])




```python
arr
```




    array([12, 11, 34, 23, 12,  8])




```python
np.in1d(arr, [11, 12])
```




    array([ True,  True, False, False,  True, False])




```python

```
