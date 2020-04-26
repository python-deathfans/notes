## 0 导语

pandas是基于numpy创建的，让numpy为中心的应用变得更加简单

只要没有加`inplace参数为True`, 所有操作都不会对元数据造成影响

## 1 Seris


```python
import pandas as pd
import numpy as np
```


```python
s = pd.Series([1, 2, 4, np.nan, 34])
s
# 默认的索引是从0开始的，可以修改index参数进行改变
```




    0     1.0
    1     2.0
    2     4.0
    3     NaN
    4    34.0
    dtype: float64



## 2 DataFrame


```python
dates = pd.date_range('2020-01-24', periods=6)

df = pd.DataFrame(np.random.randn(6, 4), index=dates, columns=list('abcd'))
df

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2020-01-24</th>
      <td>0.292231</td>
      <td>-0.527032</td>
      <td>0.425483</td>
      <td>0.621376</td>
    </tr>
    <tr>
      <th>2020-01-25</th>
      <td>0.954146</td>
      <td>0.410627</td>
      <td>-0.790093</td>
      <td>-0.450286</td>
    </tr>
    <tr>
      <th>2020-01-26</th>
      <td>-0.514790</td>
      <td>0.474891</td>
      <td>0.831309</td>
      <td>-0.665899</td>
    </tr>
    <tr>
      <th>2020-01-27</th>
      <td>-0.991812</td>
      <td>0.704291</td>
      <td>-1.155451</td>
      <td>-0.616698</td>
    </tr>
    <tr>
      <th>2020-01-28</th>
      <td>-0.079796</td>
      <td>0.021214</td>
      <td>-2.912757</td>
      <td>1.553548</td>
    </tr>
    <tr>
      <th>2020-01-29</th>
      <td>0.917742</td>
      <td>-0.501683</td>
      <td>2.884373</td>
      <td>0.367614</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['b']
```




    2020-01-24   -0.527032
    2020-01-25    0.410627
    2020-01-26    0.474891
    2020-01-27    0.704291
    2020-01-28    0.021214
    2020-01-29   -0.501683
    Freq: D, Name: b, dtype: float64




```python
df.b
```




    2020-01-24   -0.527032
    2020-01-25    0.410627
    2020-01-26    0.474891
    2020-01-27    0.704291
    2020-01-28    0.021214
    2020-01-29   -0.501683
    Freq: D, Name: b, dtype: float64




```python
# 未指定行标签和列标签的数据
df1 = pd.DataFrame(np.arange(12).reshape(3, 4))
df1
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.index
```




    DatetimeIndex(['2020-01-24', '2020-01-25', '2020-01-26', '2020-01-27',
                   '2020-01-28', '2020-01-29'],
                  dtype='datetime64[ns]', freq='D')




```python
df.columns
```




    Index(['a', 'b', 'c', 'd'], dtype='object')




```python
df.values
```




    array([[ 0.29223134, -0.52703243,  0.42548272,  0.62137609],
           [ 0.95414642,  0.41062667, -0.79009301, -0.45028615],
           [-0.51478992,  0.4748907 ,  0.83130943, -0.66589911],
           [-0.99181216,  0.70429098, -1.15545126, -0.61669812],
           [-0.07979591,  0.02121374, -2.91275711,  1.55354769],
           [ 0.9177419 , -0.50168314,  2.88437252,  0.36761414]])




```python
df.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>6.000000</td>
      <td>6.000000</td>
      <td>6.000000</td>
      <td>6.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>0.096287</td>
      <td>0.097051</td>
      <td>-0.119523</td>
      <td>0.134942</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.779421</td>
      <td>0.522216</td>
      <td>1.977345</td>
      <td>0.877724</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-0.991812</td>
      <td>-0.527032</td>
      <td>-2.912757</td>
      <td>-0.665899</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>-0.406041</td>
      <td>-0.370959</td>
      <td>-1.064112</td>
      <td>-0.575095</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>0.106218</td>
      <td>0.215920</td>
      <td>-0.182305</td>
      <td>-0.041336</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>0.761364</td>
      <td>0.458825</td>
      <td>0.729853</td>
      <td>0.557936</td>
    </tr>
    <tr>
      <th>max</th>
      <td>0.954146</td>
      <td>0.704291</td>
      <td>2.884373</td>
      <td>1.553548</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 另一种方式
df2 = pd.DataFrame({
    'A': [1,2,3,4],
    'B': pd.Timestamp('20180819'),
    'C': pd.Series([1,6,9,10],dtype='float32'),
    'D': np.array([3] * 4,dtype='int32'),
    'E': pd.Categorical(['test','train','test','train']),
    'F': 'foo'
})
print(df2)
```

       A          B     C  D      E    F
    0  1 2018-08-19   1.0  3   test  foo
    1  2 2018-08-19   6.0  3  train  foo
    2  3 2018-08-19   9.0  3   test  foo
    3  4 2018-08-19  10.0  3  train  foo
    


```python
df2.sort_index(axis=1, ascending=False )
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>F</th>
      <th>E</th>
      <th>D</th>
      <th>C</th>
      <th>B</th>
      <th>A</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>foo</td>
      <td>test</td>
      <td>3</td>
      <td>1.0</td>
      <td>2018-08-19</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>foo</td>
      <td>train</td>
      <td>3</td>
      <td>6.0</td>
      <td>2018-08-19</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>foo</td>
      <td>test</td>
      <td>3</td>
      <td>9.0</td>
      <td>2018-08-19</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>foo</td>
      <td>train</td>
      <td>3</td>
      <td>10.0</td>
      <td>2018-08-19</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2.sort_index(axis=0, ascending=False )
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2018-08-19</td>
      <td>10.0</td>
      <td>3</td>
      <td>train</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2018-08-19</td>
      <td>9.0</td>
      <td>3</td>
      <td>test</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2018-08-19</td>
      <td>6.0</td>
      <td>3</td>
      <td>train</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2018-08-19</td>
      <td>1.0</td>
      <td>3</td>
      <td>test</td>
      <td>foo</td>
    </tr>
  </tbody>
</table>
</div>




```python
df2
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>2018-08-19</td>
      <td>1.0</td>
      <td>3</td>
      <td>test</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>2018-08-19</td>
      <td>6.0</td>
      <td>3</td>
      <td>train</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>2018-08-19</td>
      <td>9.0</td>
      <td>3</td>
      <td>test</td>
      <td>foo</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>2018-08-19</td>
      <td>10.0</td>
      <td>3</td>
      <td>train</td>
      <td>foo</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 对特定列数值排列
# 表示对C列降序排列
print(df2.sort_values(by='C',ascending=False))
```

       A          B     C  D      E    F
    3  4 2018-08-19  10.0  3  train  foo
    2  3 2018-08-19   9.0  3   test  foo
    1  2 2018-08-19   6.0  3  train  foo
    0  1 2018-08-19   1.0  3   test  foo
    

## 3 pandas选择数据

### 3.1 实战筛选


```python
dates = pd.date_range('20180819', periods=6)
df = pd.DataFrame(np.arange(24).reshape(6, 4), index=dates, columns=list('ABCD'))
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-19</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2018-08-20</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>20</td>
      <td>21</td>
      <td>22</td>
      <td>23</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 列的检索
# 或者是df['A']
df.A
```




    2018-08-19     0
    2018-08-20     4
    2018-08-21     8
    2018-08-22    12
    2018-08-23    16
    2018-08-24    20
    Freq: D, Name: A, dtype: int32




```python
# 选择多行或者多列
# 选择前三行

df[:3]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-19</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2018-08-20</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 选取前三列
df.iloc[:, :3]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-19</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2018-08-20</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>20</td>
      <td>21</td>
      <td>22</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.loc[:, ['A', 'B']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-19</th>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2018-08-20</th>
      <td>4</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>12</td>
      <td>13</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>16</td>
      <td>17</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>20</td>
      <td>21</td>
    </tr>
  </tbody>
</table>
</div>




```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-19</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2018-08-20</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>20</td>
      <td>21</td>
      <td>22</td>
      <td>23</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 通过判断的筛选
df[df.A > 6]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-21</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>20</td>
      <td>21</td>
      <td>22</td>
      <td>23</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.loc[df.A > 6]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-21</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>20</td>
      <td>21</td>
      <td>22</td>
      <td>23</td>
    </tr>
  </tbody>
</table>
</div>



## 4 Pandas设置值

### 4.1 创建数据


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-19</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2018-08-20</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>11</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>20</td>
      <td>21</td>
      <td>22</td>
      <td>23</td>
    </tr>
  </tbody>
</table>
</div>



### 4.2 根据位置设置loc和iloc


```python
# iloc传入的是坐标
# loc 传入的是行和列的标签值
df.iloc[2, 2] = 111
df.loc['2018-08-20', 'B'] = 2222
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-19</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2018-08-20</th>
      <td>4</td>
      <td>2222</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>8</td>
      <td>9</td>
      <td>111</td>
      <td>11</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>20</td>
      <td>21</td>
      <td>22</td>
      <td>23</td>
    </tr>
  </tbody>
</table>
</div>



### 4.3 根据条件设置


```python
df.B[df.A > 4] = 0
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-19</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2018-08-20</th>
      <td>4</td>
      <td>2222</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>8</td>
      <td>0</td>
      <td>111</td>
      <td>11</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>12</td>
      <td>0</td>
      <td>14</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>16</td>
      <td>0</td>
      <td>18</td>
      <td>19</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>20</td>
      <td>0</td>
      <td>22</td>
      <td>23</td>
    </tr>
  </tbody>
</table>
</div>



### 4.4 按行或者列设置


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-19</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2018-08-20</th>
      <td>4</td>
      <td>2222</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>8</td>
      <td>0</td>
      <td>111</td>
      <td>11</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>12</td>
      <td>0</td>
      <td>14</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>16</td>
      <td>0</td>
      <td>18</td>
      <td>19</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>20</td>
      <td>0</td>
      <td>22</td>
      <td>23</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['F'] = np.nan
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>F</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-19</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-20</th>
      <td>4</td>
      <td>2222</td>
      <td>6</td>
      <td>7</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>8</td>
      <td>0</td>
      <td>111</td>
      <td>11</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>12</td>
      <td>0</td>
      <td>14</td>
      <td>15</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>16</td>
      <td>0</td>
      <td>18</td>
      <td>19</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>20</td>
      <td>0</td>
      <td>22</td>
      <td>23</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



### 4.5 添加Series序列（长度必须对齐）


```python
df['E'] = pd.Series([1, 2, 3, 4, 5, 6], index=pd.date_range('2018-08-19', periods=6))
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>F</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-19</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>NaN</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2018-08-20</th>
      <td>4</td>
      <td>2222</td>
      <td>6</td>
      <td>7</td>
      <td>NaN</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>8</td>
      <td>0</td>
      <td>111</td>
      <td>11</td>
      <td>NaN</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>12</td>
      <td>0</td>
      <td>14</td>
      <td>15</td>
      <td>NaN</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>16</td>
      <td>0</td>
      <td>18</td>
      <td>19</td>
      <td>NaN</td>
      <td>5</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>20</td>
      <td>0</td>
      <td>22</td>
      <td>23</td>
      <td>NaN</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>



### 4.6 修改一整行数据


```python
# 修改一整行数据
df.iloc[1] = np.nan
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>F</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-19</th>
      <td>0.0</td>
      <td>1.0</td>
      <td>2.0</td>
      <td>3.0</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2018-08-20</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>8.0</td>
      <td>0.0</td>
      <td>111.0</td>
      <td>11.0</td>
      <td>NaN</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>12.0</td>
      <td>0.0</td>
      <td>14.0</td>
      <td>15.0</td>
      <td>NaN</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>16.0</td>
      <td>0.0</td>
      <td>18.0</td>
      <td>19.0</td>
      <td>NaN</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>20.0</td>
      <td>0.0</td>
      <td>22.0</td>
      <td>23.0</td>
      <td>NaN</td>
      <td>6.0</td>
    </tr>
  </tbody>
</table>
</div>



## 5 pandas处理丢失数据

### 5.1 创建喊NAN的矩阵


```python
dates = pd.date_range('20180820',periods=6)
df = pd.DataFrame(np.arange(24).reshape((6,4)),index=dates,columns=['A','B','C','D']) 
print(df)
```

                 A   B   C   D
    2018-08-20   0   1   2   3
    2018-08-21   4   5   6   7
    2018-08-22   8   9  10  11
    2018-08-23  12  13  14  15
    2018-08-24  16  17  18  19
    2018-08-25  20  21  22  23
    


```python
df.iloc[0, 3] = np.nan
df.iloc[2, 3] = np.nan
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-20</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19.0</td>
    </tr>
    <tr>
      <th>2018-08-25</th>
      <td>20</td>
      <td>21</td>
      <td>22</td>
      <td>23.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 删除的是含有nan的行
df.dropna(
        axis=0,    # 对行进行操作
        how='any'  # any表示的是只要有就删除，all表示的是所有的都是的时候才删除
)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-21</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19.0</td>
    </tr>
    <tr>
      <th>2018-08-25</th>
      <td>20</td>
      <td>21</td>
      <td>22</td>
      <td>23.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-20</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19.0</td>
    </tr>
    <tr>
      <th>2018-08-25</th>
      <td>20</td>
      <td>21</td>
      <td>22</td>
      <td>23.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.dropna(1)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-20</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
    </tr>
    <tr>
      <th>2018-08-25</th>
      <td>20</td>
      <td>21</td>
      <td>22</td>
    </tr>
  </tbody>
</table>
</div>



### 5.2 替换nan值为其他值


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-20</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19.0</td>
    </tr>
    <tr>
      <th>2018-08-25</th>
      <td>20</td>
      <td>21</td>
      <td>22</td>
      <td>23.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.fillna(value='嘿嘿')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-20</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>嘿嘿</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>嘿嘿</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19</td>
    </tr>
    <tr>
      <th>2018-08-25</th>
      <td>20</td>
      <td>21</td>
      <td>22</td>
      <td>23</td>
    </tr>
  </tbody>
</table>
</div>




```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-20</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19.0</td>
    </tr>
    <tr>
      <th>2018-08-25</th>
      <td>20</td>
      <td>21</td>
      <td>22</td>
      <td>23.0</td>
    </tr>
  </tbody>
</table>
</div>



### 5.3 是否有缺失数据nan


```python
# 是否为空
df.isnull()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-20</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2018-08-25</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 检查是否是nan
df.isna()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-20</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>2018-08-25</th>
      <td>False</td>
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>



## 6 pandas导入导出

### 6.1 导出数据


```python
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-20</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19.0</td>
    </tr>
    <tr>
      <th>2018-08-25</th>
      <td>20</td>
      <td>21</td>
      <td>22</td>
      <td>23.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.to_csv('data.csv')
```


```python
df.to_pickle('data.pickle')
```

### 6.2 导入数据


```python
pd.read_csv('data.csv', index_col=0)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-20</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19.0</td>
    </tr>
    <tr>
      <th>2018-08-25</th>
      <td>20</td>
      <td>21</td>
      <td>22</td>
      <td>23.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.read_pickle('data.pickle')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2018-08-20</th>
      <td>0</td>
      <td>1</td>
      <td>2</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-21</th>
      <td>4</td>
      <td>5</td>
      <td>6</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>2018-08-22</th>
      <td>8</td>
      <td>9</td>
      <td>10</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2018-08-23</th>
      <td>12</td>
      <td>13</td>
      <td>14</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>2018-08-24</th>
      <td>16</td>
      <td>17</td>
      <td>18</td>
      <td>19.0</td>
    </tr>
    <tr>
      <th>2018-08-25</th>
      <td>20</td>
      <td>21</td>
      <td>22</td>
      <td>23.0</td>
    </tr>
  </tbody>
</table>
</div>



## 7 pandas合并操作

### 7.1 pandas合并之concat


```python
df1 = pd.DataFrame(np.ones((3,4))*0, columns=['a','b','c','d'])
df2 = pd.DataFrame(np.ones((3,4))*1, columns=['a','b','c','d'])
df3 = pd.DataFrame(np.ones((3,4))*2, columns=['a','b','c','d'])
```


```python
# 默认是按列进行合并
df = pd.concat([df1, df2, df3])
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>0</th>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 由于上面index有重复，可以使用ignore_index=True来修改
res = pd.concat([df1, df2, df3], ignore_index=True)
res
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# join合并方式
df1 = pd.DataFrame(np.ones((3,4))*0, columns=['a','b','c','d'], index=[1,2,3])
df2 = pd.DataFrame(np.ones((3,4))*1, columns=['b','c','d','e'], index=[2,3,4])
```


```python
"""
join="outer", 函数默认的是这个值，此方法是依照columnsl来
做纵向合并，有相同的columns上下合并，其他的独自成列，没有的值
使用nan填充
"""
df = pd.concat([df1, df2], sort=True, ignore_index=True)
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
"""
join="inner"
表示的是内连接，相同的
column进行纵向合并
"""

res = pd.concat([df1, df2], join='inner', sort=True, ignore_index=True)
res
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
