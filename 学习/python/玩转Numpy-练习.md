```python
import numpy as np
```

## 打印版本和配置信息


```python
np.__version__
```




    '1.18.1'



## 创建一个长度为10的空向量


```python
z = np.zeros(10)
z
```




    array([0., 0., 0., 0., 0., 0., 0., 0., 0., 0.])



## 找到任何一个数组的内存大小


```python
z = np.zeros((10, 10))
print("%d bytes" % (z.size * z.itemsize))
```

    800 bytes
    

## 如何从命令行得到numpy中add函数的说明文档


```python
np.info(np.add)
```

    add(x1, x2, /, out=None, *, where=True, casting='same_kind', order='K', dtype=None, subok=True[, signature, extobj])
    
    Add arguments element-wise.
    
    Parameters
    ----------
    x1, x2 : array_like
        The arrays to be added. If ``x1.shape != x2.shape``, they must be broadcastable to a common shape (which becomes the shape of the output).
    out : ndarray, None, or tuple of ndarray and None, optional
        A location into which the result is stored. If provided, it must have
        a shape that the inputs broadcast to. If not provided or None,
        a freshly-allocated array is returned. A tuple (possible only as a
        keyword argument) must have length equal to the number of outputs.
    where : array_like, optional
        This condition is broadcast over the input. At locations where the
        condition is True, the `out` array will be set to the ufunc result.
        Elsewhere, the `out` array will retain its original value.
        Note that if an uninitialized `out` array is created via the default
        ``out=None``, locations within it where the condition is False will
        remain uninitialized.
    **kwargs
        For other keyword-only arguments, see the
        :ref:`ufunc docs <ufuncs.kwargs>`.
    
    Returns
    -------
    add : ndarray or scalar
        The sum of `x1` and `x2`, element-wise.
        This is a scalar if both `x1` and `x2` are scalars.
    
    Notes
    -----
    Equivalent to `x1` + `x2` in terms of array broadcasting.
    
    Examples
    --------
    >>> np.add(1.0, 4.0)
    5.0
    >>> x1 = np.arange(9.0).reshape((3, 3))
    >>> x2 = np.arange(3.0)
    >>> np.add(x1, x2)
    array([[  0.,   2.,   4.],
           [  3.,   5.,   7.],
           [  6.,   8.,  10.]])
    

## 创建一个长度为10并且除了第五个值为1的空向量


```python
z = np.zeros(10)
z[4] = 1
z
```




    array([0., 0., 0., 0., 1., 0., 0., 0., 0., 0.])



## 创建一个从10到49的向量


```python
z = np.arange(10, 50)
z
```




    array([10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26,
           27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43,
           44, 45, 46, 47, 48, 49])



## 翻转一个向量（第一个变成最后一个）


```python
z = np.arange(30)
z = z[::-1]
z
```




    array([29, 28, 27, 26, 25, 24, 23, 22, 21, 20, 19, 18, 17, 16, 15, 14, 13,
           12, 11, 10,  9,  8,  7,  6,  5,  4,  3,  2,  1,  0])



## 创建一个3x3并且值从0到8的矩阵


```python
z = np.arange(9).reshape(3, 3)
z
```




    array([[0, 1, 2],
           [3, 4, 5],
           [6, 7, 8]])



## 找到数组[1,2,0,0,4,0]中非0元素的位置索引


```python
not_zero = np.nonzero([1, 2, 0, 0, 4, 0])
not_zero
```




    (array([0, 1, 4], dtype=int64),)



## 创建一个3x3的单位矩阵


```python
z = np.eye(3)
z
```




    array([[1., 0., 0.],
           [0., 1., 0.],
           [0., 0., 1.]])



## 创建一个3x3x3的随机数组


```python
z = np.random.random((3, 3, 3))
z
```




    array([[[0.2008754 , 0.50914001, 0.83579415],
            [0.02394748, 0.73147829, 0.50228816],
            [0.48512456, 0.49663092, 0.60866792]],
    
           [[0.26972622, 0.82654455, 0.8551261 ],
            [0.99106156, 0.79979487, 0.76306868],
            [0.8855042 , 0.30093917, 0.54658407]],
    
           [[0.12334509, 0.01277733, 0.88075059],
            [0.43481045, 0.08331349, 0.59241245],
            [0.93578235, 0.15751609, 0.80830804]]])



## 创建一个10x10的随机数组并且找到最大值和最小值


```python
z = np.random.random((10, 10))
z_min, z_max = np.min(z), np.max(z)
print(z_min, z_max)
```

    0.0007838674500245668 0.9704474562862483
    

## 对于一个存在的数组，如何添加一个用0填充的边界}


```python
z = np.ones((5, 5))
z = np.pad(z, pad_width=1, mode='constant', constant_values=0)
z
```




    array([[0., 0., 0., 0., 0., 0., 0.],
           [0., 1., 1., 1., 1., 1., 0.],
           [0., 1., 1., 1., 1., 1., 0.],
           [0., 1., 1., 1., 1., 1., 0.],
           [0., 1., 1., 1., 1., 1., 0.],
           [0., 1., 1., 1., 1., 1., 0.],
           [0., 0., 0., 0., 0., 0., 0.]])



## 考虑一个(6,7,8)形状的数组，第100个元素的索引是什么


```python
np.unravel_index(100, (6,7,8))
```




    (1, 5, 4)



## 给定一个一维数组，对其3到8之间的所有元素取反


```python
z = np.arange(11)

z[(3<=z)&(z<=8)] *= -1
z
```




    array([ 0,  1,  2, -3, -4, -5, -6, -7, -8,  9, 10])



## 找到两个数组中共同元素


```python
z1 = np.random.randint(0, 10, 10)
z2 = np.random.randint(0, 10, 10)
np.intersect1d(z1, z2)
```




    array([1, 3, 4, 7, 8])



## 如何得到昨天、今天、明天的日期


```python
yesterday = np.datetime64('today', 'D') - np.timedelta64(1, 'D')
today = np.datetime64('today', 'D')
tomorrow = today + np.timedelta64(1, 'D')

print("today:{}".format(today))
```

    today:2020-02-14
    

## 如何得到与2016年7月对应的日期


```python

```

## 创建一个5x5的矩阵， 其中每行的数值范围是0到4


```python
z = np.zeros((5, 5))
z += np.arange(5)
z
```




    array([[0., 1., 2., 3., 4.],
           [0., 1., 2., 3., 4.],
           [0., 1., 2., 3., 4.],
           [0., 1., 2., 3., 4.],
           [0., 1., 2., 3., 4.]])



## 通过考虑一个可生成10个整数的函数，来构建一个数组


```python
def generate():
    for x in range(10):
        yield x

        
z = np.fromiter(generate(), dtype=float)
z
```




    array([0., 1., 2., 3., 4., 5., 6., 7., 8., 9.])



## 创建一个长度为10的随机向量，治愈范围0,1，但是不包括0和1


```python
z = np.linspace(0, 1, 11, endpoint=False)[1:]
z
```




    array([0.09090909, 0.18181818, 0.27272727, 0.36363636, 0.45454545,
           0.54545455, 0.63636364, 0.72727273, 0.81818182, 0.90909091])



## 创建一个长度为10的随机向量，并排序


```python
z = np.random.random(10)
z.sort()
z
```




    array([0.12159468, 0.16240543, 0.21079394, 0.27399265, 0.34133772,
           0.51466898, 0.58353379, 0.72351169, 0.9097548 , 0.97051432])



## 对于一个小数组，如何用比np.sum更快的方式对其进行求和


```python
z = np.arange(10)

np.add.reduce(z)
```




    45



## 创建一个只读数组


```python
z = np.zeros(5)
z.flags.writeable =False
try:
    z[0] = 1
except Exception as e:
    print("不能写入啦：%s" % e)
```

    不能写入啦：assignment destination is read-only
    

## 创建一个长度为10的向量，将最大值替换为1


```python
z = np.random.random(10)
z[z.argmax()] = 1
z
```




    array([0.23045758, 0.23987609, 0.85074855, 0.89221275, 0.90861406,
           1.        , 0.93215616, 0.90764512, 0.25026604, 0.52202815])



## 对于numpy数组，enumerate的等价操作是什么


```python
z = np.arange(9).reshape(3, 3)

for index, value in np.ndenumerate(z):
    print(index, value)
```

    (0, 0) 0
    (0, 1) 1
    (0, 2) 2
    (1, 0) 3
    (1, 1) 4
    (1, 2) 5
    (2, 0) 6
    (2, 1) 7
    (2, 2) 8
    

## 减去每行的平均值


```python
x = np.random.rand(5, 10)
y = x - x.mean(axis=1, keepdims=True)
y.shape
```




    (5, 10)



## 通过第n列队一个数组进行排序


```python
z = np.random.randint(0, 10, (3, 3))
print(z[z[:, 1].argsort()])
```

    [[4 2 9]
     [3 4 5]
     [9 7 3]]
    

## 根据索引列表(I), 如何将向量(x)的元素累加到数组(F)


```python
x = [1, 2, 4, 5, 6, 9]
I = [1, 3, 9, 1, 6, 7]
F = np.bincount(I, x)
F
```




    array([0., 6., 0., 2., 0., 0., 6., 9., 0., 4.])



## 找到一个数组中出现频率最高的值


```python
np.random.seed(3)
z = np.random.randint(0, 10, 50)
print(z)

np.bincount(z).argmax()
```

    [8 9 3 8 8 0 5 3 9 9 5 7 6 0 4 7 8 1 6 2 2 1 3 5 8 1 8 7 8 1 0 5 4 1 5 4 7
     6 0 0 9 2 4 5 8 8 7 5 1 1]
    




    8




```python

```


```python

```
