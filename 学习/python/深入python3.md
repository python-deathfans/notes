## 处理文件和目录

- [x] **import os**
- os.getcwd()
  - 获取当前工作目录
- os.path.exits()
  - 测试路径是否存在
- os.path.isdir()
  - 测试路径是否是一个存在的目录
- os.path.join(path, filename)
  - 可以拼接成一个新的路径
- os.path.split()
  - 把路径和文件分开
- os.path.splittext()
  - 把文件名和扩展名分开
- os.path.realpath(filename)
  - 返回文件的绝对路径

- [x] import glob
- glob.glob()
  - 支持通配符搜搜

## 解析式

+ **列表解析式**
  + [x**2 for x in range(4) if x%2 == 0]
+ **字典解析式**
  + {k:v for k,v in a_dict.items()}
+ **集合解析式**
  + 类似于列表解析式

## 字符串

+ **unicode编码**
  + 使用`４个字节`的数字来表达每个字母、符号，或者表意文字。
+ **string vs bytes**
  + 每个string都对应一个encode方法，可以使得string变成bytes
  + 同样每个bytes都有一个decode方法，可以使得bytes变成string

## 生成器和迭代器

+ 迭代器
  + 是python最强大的功能之一，是访问集合元素的一种方式
  + 迭代器可以记住遍历位置的对象
  + 有两个基本方法:**iter()**和**next()**
  + 字符串，列表或元祖对象都可以用于创建迭代器
  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-02-28_10-17-22.png" style="zoom: 80%;" align="center" />
  + 迭代器对象也可以使用for语句进行遍历
    + ![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-02-28_10-35-23.png)

```python
def make_counter(x):
    print("entering the make_counter")

    while True:
        yield x

        print("x increment 1")
        x += 1
```

+ 含有yield的函数证明不是一个普通函数，而是一个生成器函数，而且一次只产生一个值，使用next方法进行反复调用
+ 理论上这个函数可以无限执行，所以还是看一个更加实用的例子吧

```python
def fib(max):
    a, b = 0, 1

    while a<max:
        yield a
        a, b = b, a+b
```

