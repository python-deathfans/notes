[TOC]



## python变量以及内存管理机制

>内容概览：
>
>+ 引用与对象
>+ 可变数据类型与不可变数据类型
>+ 引用传递与值传递
>+ 深拷贝与浅拷贝

### python中的变量

+ 引用与对象

  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-24_10-09-25.png" style="zoom:80%;" />
  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-24_10-11-04.png" style="zoom:80%;" />

  + 对象：

    + 当创建数据对象时，在内存中会保存对象的值

  + 引用

    + 对象保存在内存空间中，外部想要使用，需要使用引用，就是‘name1’,'name2'.内存会保存对象的引用数量，当引用为0的时候，对象会被收回(这个信息放在对象的头部信息中)

  + ```python
    import sys
    
    a = 34
    print(sys.getrefcount(a))	# 结果比期望多1个，python会创建一个临时的引用
    ```

  + **引用对象增加**

    + 对象被创建
    + 另外的别人被创建
    + 作为容器的一个元素
    + 被作为参数传递给函数

  + **引用对象减少**

    + 对象的别名被显式销毁
    + 对象的一个别名被赋给其他对象
    + 对象离开自身的作用域

  + 容器对象

    + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-24_10-48-49.png" style="zoom:80%;" />

+ 可变类型与不可变类型

  + 可变类型：列表，字典
    + **内存中可以保存两个相同的对象**
  + 不可变类型：整型、浮点型、字符串、元组
    + **内存中不能保存两个相同的对象**，比如a = 2, b = 2, 这里a、b的地址是一样的
  + 这里的可变、不可变是指**内存中的那块内容**是否可变

+ 深拷贝与浅拷贝

  + 赋值拷贝
    + 只是创建一个变量，还是指向原来的地址
    + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-24_11-17-13.png" style="zoom:80%;" />

+ 浅拷贝
  + 只创建第一层的数据，其他的都是引用
  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-24_11-18-23.png" style="zoom:80%;" />

+ 深拷贝

  + 除了最后一层的数据不会创建，其余都会创建

  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-24_11-19-16.png" style="zoom:80%;" />

## printf函数格式化输出

+ 两种用法：

  + %用法
    + %o	八进制输出

    	 %d	十进制输出

    	 %x	十六进制输出

    	 %s	字符串输出

    	 %c	字符输出

  + format用法

![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\图片2.png)



![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\图片3.png "format实例")



## 序列

+ 类型
  + 字符串
  
  + 列表

    + **删除元素**
      + **remove** 删除的元素
      + **pop**  指定位置删除元素
      + **clear**  清空列表元素
  
    + **排序**
  
      + **sorted**函数（data, key= , reverse= ,）
        + data是传入的序列，返回一个新的，不会对原序列产生影响
        + reverse=True 参数声明升序还是降序
        + key=len 根据字符串的长度进行排序而不是默认的字母表排序
  
      + **data.sort**(reverse=True)
  
  + 元祖
  
+ 操作符

  + 成员关系操作符（in not in）

  + 连接操作符（+）

  + 重复操作符(*)

  + 切片操作符([],[:],[::])

  + 用步长索引进行切片

    + ```python
      s = 'abcdefg'
      
      a = s[::-1]	## 翻转
      b = s[::2]  ## 隔一个取一个
      ```


## 字典

+ 创建

  + ```python
    scores = {'骆昊': 95, '白元芳': 78, '狄仁杰': 82}
    ```

  + ```python
    items1 = dict(one=1, two=2, three=3, four=4)
    ```

  + ```python
    items2 = dict(zip(['a', 'b', 'c'], '123'))
    ```

  + ```python
    items3 = {num: num ** 2 for num in range(1, 10)}
    ```

+ 删除
  + **popitem**
  + **pop**
  + **clear**

+ 遍历

  + ```python
    dic = {'key':'value'}
    
    for key in dic:
    	print("%s --> %s" % (key, dic[key]))
    ```

  + ```python
    dic = {'key':'value'}
    
    for key,item in dic.items():
    	print("%s --> %s" % (key, value))
    ```

    

## time模块

```python
import time

timestamp = time.time()
timestruct = time.localtime(time.time())
currenttime = time.asctime(time.localtime(time.time()))

print('当前的时间戳是:',timestamp)
print("当前时间是:",timestruct)
print('现在时间是:',currenttime)


"""
the result is :
当前的时间戳是: 1569047092.1938396
当前时间是: time.struct_time(tm_year=2019, tm_mon=9, tm_mday=21, tm_hour=14, tm_min=24, tm_sec=52, tm_wday=5, tm_yday=264, tm_isdst=0)
现在时间是: Sat Sep 21 14:24:52 2019
"""

```



```python
import time
 
# 格式化成2016-03-20 11:45:39形式
print (time.strftime("%Y-%m-%d %H:%M:%S", time.localtime()) )
 
# 格式化成Sat Mar 28 22:24:24 2016形式
print (time.strftime("%a %b %d %H:%M:%S %Y", time.localtime()) )
  
# 将格式字符串转换为时间戳
a = "Sat Mar 28 22:24:24 2016"
print (time.mktime(time.strptime(a,"%a %b %d %H:%M:%S %Y")))

"""
the result is :
2019-09-21 14:26:55
Sat Sep 21 14:26:55 2019
1459175064.0

"""

```



```python
import calendar
 
cal = calendar.month(2016, 1)
print ("以下输出2016年1月份的日历:")
print (cal)

"""
the result is :
以下输出2016年1月份的日历:
    January 2016
Mo Tu We Th Fr Sa Su
             1  2  3
 4  5  6  7  8  9 10
11 12 13 14 15 16 17
18 19 20 21 22 23 24
25 26 27 28 29 30 31

"""
```



## OS模块

```python
import os

# ../ 当前目录的上一级目录

# 返回当前工作路径
# 绝对路径

# res = os.getcwd()
# print(res)

# 返回指定路径下的文件和文件夹

res = os.listdir()
print(res)

# 创建文件夹
os.mkdir()

# 创建多级文件夹
os.makedirs()

# 删除文件夹
os.rmdir()

# 改变工作路径
os.chdir()

# 分割路径和文件，返回类型是元祖
res = os.path.split()
print(res)

# 拼接目录和文件名
# 需要两个参数
os.path.join()

# 判断一个路径是否存在
os.path.exists()

# 返回文件名和后缀
os.path.splittext()

# 返回文件的绝对路径
os.path.realpath()
```



## 文件操作

+ 输入
  + **read()**
    + 读取所有的文件，返回一个**字符串**
  + **readlines()**
    + 读取所有(剩余)的内容，返回一个**列表**
  + **readline()**
    + 读取到下一行，返回一个**字符串**



## sys模块

+ **sys.argv[]**
  + 主要用来从外部获取程序运行的参数，下标为0的时候显示的是第一个参数，以此类推



## 函数

```python
# 闭包：调用一个函数，返回一个函数回来，返回的函数叫做闭包
# 闭包函数使用外部函数的前提是 内部没有这个变量


def outer(num1):
    def inner(num2):
        return num1 + num2
    return inner


res = outer(20)     # res = inner,inner是函数名字
result = res(10)

print(result)
```

```python
# args是不定长参数，类型是元祖，不需要关心给多长的参数，可以直接遍历
def sum(*args):
    sum = 0

    for var in args:
        sum += var

    return sum

res = sum(1, 2, 3, 55)

print(res)
```

```python
# kwargs可以接受不定长关键字参数
# 关键字参数如 a = 3,b = 5这种类型
# kwargs类型是字典
def func(**kwargs):
    print(kwargs)

func(a = 3, b = 65, df = 543)
```

+ 函数参数

  + `必要参数`

    + ```python
      def say(s):
      	print("i am %s" % s)
      ```

  + `默认参数`

    ```python
    def add(a=1, b=2):
    	return a+b
    ```

  + `可变参数(不定长参数)`

    + ```python
      def say(age, *som):
      	print("i am %d  old" % age)
      	
      	for i in som:
      		print(i)
      ```

  + `关键字参数(**),传入的必须是字典`

    + 默认参数的形式进行传递，如 **i=2**

+ 由于PYTHON中没有**函数重载**，所以实际上**不能存在两个同名的函数**，后面的会把前面的屏蔽掉，所以为了避免这种事情，可以使用模块进行函数的管理，特别是项目里面，两个模块使用同一个函数名，通过导入，可以避免这种情况发生。

  `module1.py`

  ```python
  def foo():
  	printf("hello, world!")
  ```

  `module2.py`

  ```python
  def foo():
  	printf("goobye, world!")
  ```

  `test.py`

  ```python
  import module1 as m1
  import module2 as m2
  
  m1.foo()
  m2.foo()
  ```

+ 如果我们导入的模块除了**定义函数之外**还中有可以执行代码，那么Python解释器在导入这个模块时就会执行这些代码，事实上我们可能并不希望如此，因此如果我们在模块中编写了执行代码，最好是将这些执行代码放入如下所示的条件中，这样的话除非直接运行该模块，if条件下的这些代码是不会执行的，因为只有直接执行的模块的名字才是"__main__"。 

  ​		``model3.py``

  ```python
  def foo():
  	pass
  
  def bar():
  	pass
  	
  # __name__ 是python中一个隐含的变量，它代表模块的名字
  # 只有被python解释器直接直接的模块的名字才是__main__
  if __name__ == '__main__':
  	print("call foo()")
  	foo()
  	
  	print("call bar()")
  	bar()
  ```

+ **变量作用域**

  + 在接口中定义的变量是全局变量，所有的函数内部都可以访问到

  + 局部变量，只能在函数内容进行访问

  + 嵌套变量，只能在嵌套范围内进行访问

  + 如果想要在函数内部修改全局变量，可以使用global关键字，例如 global a,如果a不是全局变量，那么下面的代码就可以定义变量a并将其置为全局变量

  + 所以，一般的代码需要写成下面的格式：

    + ```python
      def main():
      	# add your code here
      	pass
      
      if __name__ == '__main__':
      	main()
      ```

      

## 面向对象

+ 基本概念
  + 类：用来描述具有相同属性和方法的对象集合
  + 类变量：类变量在整个实例化中是公有的
  + 实例变量：定义在方法中的变量，只作用于当前实例的类
  
+ 内存中的存储
  
+ ![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-22_10-49-31.png)
  
+ <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-22_11-06-05.png" style="zoom:80%;" />
  + 普通字段属于对象
  + 静态字段属于类
  
+ **属性其实是普通方法的变种**

  + 定义

  + 调用

    + ```python
      class Person(object):
          """构造一个人类的对象"""
      
          count = 0
      
          @property
          def noise(self):
              return 'tall noise'
      
      
      xh = Person()
      
      # 调用，不需要加上括号
      # property装饰器可以使得方法变成属性，调用起来一样一样的
      print(xh.noise)
      ```

```python
class Person:

    def __init__(self, name, age):
        self.name = name
        self.__age = age

    def getage(self):
        print(self.__age)

    def setage(self):
        age = int(input("请输入新的年龄:"))
        self.__age = age

    # 把私有属性变成和公有属性一样访问
    @property
    def age(self):
        return self.__age

    # 把私有属性的修改方式改成和公有属性一样
    @age.setter
    def age(self, age):
        self.__age = age


zhagnsan = Person("张三", 13)

zhagnsan.name = "李四"

print(zhagnsan.age)

zhagnsan.age = 23
print(zhagnsan.age)

```

+ 一般来说，我们希望**属性是私有**的，外部没法访问，**方法是公有**的，外部可以通过方法给属性进行传值，python中**私有属性**只需要在前面加入两个_即可。单个的下划线表示属性是受保护的，因为私有属性在继承的时候没法继承过去。
  
+ 封装
  + 隐藏一切可以隐藏的细节，只向外界暴露简单的编程接口。
  + 我们在类中定义的方法说白了就是把数据和对于数据的操作封装起来，在我们创建了对象之后，只需要给对象发送一个消息，就可以执行方法中的代码

+ **@property装饰器**

  + 这时就可以使用 `property` 工具，**它把方法包装成属性，让方法可以以属性的形式被访问和调用**。

  + 被 @property 装饰的方法是**获取属性值**的方法，被装饰方法的名字会被用做 `属性名`。

  + 被 @`属性名.setter` 装饰的方法是**设置属性值**的方法。

  + 被 `@属性名.deleter` 装饰的方法是**删除属性值**的方法。

  + ```python
  """
    2020年1月15日06:51:44
    学习property装饰器的使用
    包括setter方法、getter方法
    主要是可以使得被装饰的函数名变成属性
    """
    class Student:
        def __init__(self):
            self._age = None
    
        # getter方法，注意函数名字被当成属性
        @property
        def age(self):
            print("属性被获取时调用")
    
            return self._age
    
        # setter方法
        @age.setter
        def age(self, age):
            print("属性被设置时调用")
            self._age = age
    
        # deleter方法
        @age.deleter
        def age(self):
            print("属性被删除时调用")
            del self._age
    
    if __name__ == '__main__':
        s = Student()
    
        s.age = 13
        del s.age
        
    
    ```
  
+ property函数

  +  `property(fget=None, fset=None, fdel=None, doc=None) -> property attribute` 

  + ```python
    """
    2020年1月15日06:09:17
    练习property的使用
    """
    class Student:
        def __init__(self):
            self._age = None
    
        def get_age(self):
            print("获取属性时执行的代码")
    
            return self._age
    
        def set_age(self, age):
            print("设置属性时执行的代码")
            self._age = age
    
        def del_age(self):
            print("删除属性时执行的代码")
            del self._age
    
        age = property(get_age, set_age, del_age, "学生年龄")
    
    if __name__ == '__main__':
    
        s = Student()
    
        # 注意用 类名.属性.__doc__ 的形式查看属性的文档字符串
    
        print("查看属性的文档字符串:" + Student.age.__doc__)
        """
        查看属性的文档字符串:学生年龄
        """
    
        s.age = 18
        """
        设置属性时执行的代码
    """
    
    
    ```

+ slots魔法

  + 因为python是动态语言，所以可以动态的添加属性，slots魔法可以限制绑定的属性

  + ```python
    """
    2020年1月15日07:06:12
    学习slots魔法
    """
    class Person:
        __slots__ = ("_name", "_age", "_gender", "_salary")
    
        def __init__(self, name, age):
            self._name = name
            self._age = age
    
        @property
        def name(self):
            return self._name
    
        @property
        def age(self):
            return self._age
    
        @age.setter
        def age(self, age):
            self._age = age
    
        def play(self):
            if self._age <= 16:
                print("{}正在玩飞行棋".format(self._name))
            else:
                print("{}正在玩斗地主".format(self._name))
    
    
    p = Person("王大锤", 22)
    p.play()
    
    p._gender = "男"
    p.age = 12
    p.play()
    
    p._salary = 100
    ```

+ 类的特殊成员(全部是双下划线)
  
  + __doc__
    + 表示类的描述信息
  + __module__
    + 表示当前操作的那个对象在哪个**模块**
  + __class__
    + 表示当前操作的对象的**类**是什么
  + __dict__
    + 类或对象中的所有**成员**
  + __str__
    + 如果定义了该方法，那么打印对象的时候默认打印这个函数的返回值
  + __iter__
    + 用于迭代器，之所以列表、字典、元组可以及进行for循环，是因为内部定义了这个方法
  
+ hasattr and getattr
  
  + 第一个查看对象是否有某个属性
  + 第二个查看对象属性值

## 装饰器

+ 定义
  + 用于拓展原来函数功能的一种函数，目的是在不改变函数名（或者类名）的情况下，给函数增加新的功能

+ 特点
  + 返回值是一个函数，这个函数是内嵌“原”函数的函数（函数闭包）

```python
#  在不改变函数的情况下，给函数增加一个功能
#  装饰器也叫语法糖
#  装饰器必须是闭包

import time


def outer(func):
    def inner():
        start = time.time()
        func()
        run = time.time() - start

        print(run)
    return inner


@outer
def func():
    for i in range(1000000):
        pass
    print('hello')


func()
```

## 包的导入

+ 在pycharm项目中，点击new python package

+ 包必须包含(——init——)文件

+ 如果需要在外部导入模块，需要在init文件下指定需要外界引用的模块

  + ```python
    from . import send_message
    ```

    

## 匿名函数

+ 语法
  
+ lambda参数:表达式
  
+ lambda函数+filter函数 

  + ```python
    my_list = [2,3,4,5,6]
    new_list = list(filter(lambda x:(x/3==2), my_list))
    print(new_list)
    ```

+ lambda函数+map函数

  + ```python
    my_list = [2,3,4,5,6,7,8]
    new_list = list(map(lambda x:(x/3 != 2), my_list))
    print(new_list)
    ```

    





## 操作数据库（mysql）

```python
# 创建数据表
import pymysql

conn = pymysql.connect(
                host = '127.0.0.1',
                port = 3306,
                user = 'root',
                passwd = '138210',
                db = 'mydatabase',
                charset = 'utf8'
)

cur = conn.cursor()

cur.execute('drop table if exists Emp') # 假如emp表存在就删除

sql = """
    create table Emp
    (
        first_name char(20) not null,
        last_name char(20),
        age int,
        sex char(1),
        income float
    )
"""

cur.execute(sql)

cur.close()
conn.close()
```

```python
# 数据库连接
import pymysql

conn = pymysql.connect(host = '127.0.0.1',
                        port = 3306,
                        user = 'root',
                        passwd = '138210',
                        db = 'mydatabase',
                        charset = 'utf8'
)

cur = conn.cursor()

cur.execute("select version()")

data = cur.fetchone()

print(conn)
print(cur)
print("database version :%s" % data)

cur.close()
conn.close()
```

```python
# 插入 更新 删除操作
import pymysql

conn = pymysql.connect(
                host = '127.0.0.1',
                port = 3306,
                user = 'root',
                passwd = '138210',
                db = 'mydatabase',
                charset = 'utf8'
)

cur = conn.cursor()

# 插入操作时候，数据一定要加单引号，否则报错
sql_insert = "insert into user values('name5',5)"
sql_update = "update user set userid = 44 where username = 'name4'"
sql_delete = "delete from user where username = 'name5'"

try:

    cur.execute(sql_insert)
    print(cur.rowcount)

    cur.execute(sql_update)
    print(cur.rowcount)

    cur.execute(sql_delete)
    print(cur.rowcount)

    conn.commit()
except Exception as e:
    print(e)
    conn.rollback()
finally:
    cur.close()
    conn.close()
```



## pyinstaller 打包软件

+ **pyinstaller -F name.py**
  		打包name.py为可执行程序，前提是目录中有这个代码
+ **pyinstaller -F name.py --noconsole**
  		打包name.py为可执行程序，前提是目录中有这个代码，并且运行的程序没有**dos窗口**



## 图片处理PIL库

### Tips

+ 读入的是一个**对象**，不是一个**array**

+ 想转成array,需要**np.array(imag)**

+ **channel last**

+ ```python
  #矩阵再转为图像
  new_im = Image.fromarray(arr)
  new_im.save('3.png')
  ```

  

```python
# 打开图片
from PIL import Image

imgpath = r'./石原里美/5.jpg'

image = Image.open(imgpath)
image.show()
```

```python
# 保存图片
from PIL import Image

imagepath = r'./石原里美/5.jpg'

image = Image.open(imagepath)

print(image.format, image.size, image.mode)

image.save('1.png')
print("图片保存成功")
```

```python
# 新建图片
from PIL import Image

# 第一个参数是mode,第二个参数是size，第三个参数是color
newimg = Image.new("P", (128, 128), "red")
newimg.show()
```

![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2019-11-10_09-15-43.png)

```python
# 图片旋转
from PIL import Image
import os

# 将路径移动到所在的文件夹
os.chdir(r'C:\Users\Administrator\Desktop\file\日常学习\python学习笔记\图片处理PIL库')

img = Image.open("2.png")
img_45 = img.rotate(45)
img_30 = img.rotate(30, Image.NEAREST, 1)

img_45.save("img_45.png")
img_30.save("img_30.png")

# 打印图片的尺寸(分辨率)
print(img_30.size, img_45.size)
```

```python
# 图线裁剪
from PIL import Image

img = Image.open(r'1.png')
print(img.size)

box = (100, 100, 500, 500)

# 传入的是一个四元组
region = img.crop(box)
region.show()
```

```python
# convert模式转换
from PIL import Image

img = Image.open('2.jpg')

# 将图片转换成灰度图
newimg1 = img.convert("P")
# 将图片抓换成像素图片
newimg2 = img.convert("1")
newimg1.save("1_P.png")
newimg2.save("1_1.png")

print("图片保存成功")
```

```python
# draft返回相近大小的图片
from PIL import Image

img = Image.open(r'1.jpeg')
print(img.size, img.mode)

new_img = img.draft("L", (100, 100))
print(new_img)
```

```python
# filter图片过滤器
from PIL import Image
from PIL import ImageFilter

img = Image.open(r'2.png')

blurimg = img.filter(ImageFilter.BLUR)  # 均值滤波(类似加了个滤镜，图像模糊)
edgeimg = img.filter(ImageFilter.FIND_EDGES)    # 边缘检测(不是很好看，图像发黑)
contourimg = img.filter(ImageFilter.CONTOUR)    # 寻找轮廓（类似于手绘图片）

blurimg.save("blur.png")
edgeimg.save("edge.png")
contourimg.save("contour.png")


blurimg.show()
edgeimg.show()
contourimg.show()

```

```python
# blend图片合成
from PIL import Image

img1 = Image.open(r'1.png')
img2 = Image.open(r'2.png')

size = (600,600)

img1 = img1.resize(size,Image.ANTIALIAS)
img2 = img2.resize(size,Image.ANTIALIAS)

# 合成公式 newimg = img1*(1-alpha) + img2 * alpha
blendimg = Image.blend(img1, img2, 0.5)

blendimg.show()
```

```python
# split通道分离
from PIL import Image

img = Image.open(r'1.png')

r, g, b = img.split()

print(r, g, b)
```

```python
# thumbnail图像缩略图
from PIL import Image

img = Image.open("1.jpg")

print(img.size)

img.thumbnail((400,400))
img.save("thumbnail.jpg")

print(img.size)
```

```python
# 图像paste
from PIL import Image

img = Image.open(r'1.png')

box = (0, 0, 100, 100)

region = img.crop(box)
print(region.size)

img.paste(region)
img.paste(region, (300, 300))
img.show()
```

```python
# 图片拼接
from PIL import Image
import os

if __name__ == '__main__':

    x = 0
    y = 0

    os.chdir(r"C:\Users\Administrator\Desktop\file\日常学习\python学习笔记\图片处理PIL库")

    imgs = os.listdir(r'.\石原里美')

    newimag = Image.new('RGB', (1000, 1000))
    width = 250
    LineNum = 4

    for i in imgs:
        img = Image.open('.//石原里美//' + i)
        img = img.resize((width, width), Image.ANTIALIAS)
        # print(img.size)
        newimag.paste(img, (x * width, y * width))
        x += 1

        if x == LineNum:
            x = 0
            y += 1
    newimag.save('10.jpg')
    print('拼接成功')
```



## cv库图片处理

```python
# 图片读取和显示
import cv2

imgRGB = cv2.imread("1.jpg")

cv2.namedWindow("image")
cv2.imshow("image", imgRGB)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

```python
# 漫画风格
import cv2

imgRGB = cv2.imread("1.jpg")
imgGray = cv2.cvtColor(imgRGB, cv2.COLOR_RGB2GRAY)
imgGray = cv2.medianBlur(imgGray,5)

img_edge = cv2.adaptiveThreshold(
                        imgGray, 255,
                        cv2.ADAPTIVE_THRESH_MEAN_C,
                        cv2.THRESH_BINARY, blockSize=3, C=2
)
cv2.imwrite("3.jpg", img_edge)

```

```python
# 写实风格
import cv2

imgRGB = cv2.imread("1.jpg")
imgGray = cv2.cvtColor(imgRGB, cv2.COLOR_RGB2GRAY)
imgBlur = cv2.GaussianBlur(imgGray, ksize=(21, 21), sigmaX=0, sigmaY=0)

imgReal = cv2.divide(imgGray, imgBlur, scale=255)

cv2.imwrite("5.jpg", imgReal)
```



## GUI tkinter

```python
#  主窗体生成
import tkinter as tk

# 生成一个Tk对象（也叫主窗体对象）
root = tk.Tk()

# 设置窗体的名称
root.title("GUI第一弹")

# 设置窗体的大小，中间的是小写的x
root.geometry("300x300")
root['background'] = "pink"

# 让窗体循环起来，窗体才会一直显示
root.mainloop()

```

```python
# entry控件
import tkinter as tk

# 生成一个Tk对象（也叫主窗体对象）
root = tk.Tk()

# 设置窗体的名称
root.title("GUI第四弹 entry控件")

# 设置窗体的大小，中间的是小写的x
root.geometry("300x300")
root['background'] = "pink"

# 第一个参数主要是说明控件的父窗口是谁

entry = tk.Entry(root, bg="green", fg="white", show="*")
entry.pack()

# 让窗体循环起来，窗体才会一直显示
root.mainloop()

```

![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2019-11-10_09-56-05.png "entry控件属性")

```python
# Label控件
import tkinter as tk

# 生成一个Tk对象（也叫主窗体对象）
root = tk.Tk()

# 设置窗体的名称
root.title("GUI第一弹")

# 设置窗体的大小，中间的是小写的x
root.geometry("300x300")

root['background'] = "pink"

# 第一个参数主要是说明控件的父窗口是谁
# text属性是控件上面的文字
label = tk.Label(root, text="你好啊，我是Label控件", bg="orange", fg="white", font="楷体")
label.pack()

# 让窗体循环起来，窗体才会一直显示
root.mainloop()
```

![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2019-11-10_09-59-56.png "Label控件属性")

```python
# text控件
import tkinter as tk

# 生成一个Tk对象（也叫主窗体对象）
root = tk.Tk()

# 设置窗体的名称
root.title("GUI第五弹 text控件")

# 设置窗体的大小，中间的是小写的x
root.geometry("300x300")

root['background'] = "pink"

# 第一个参数主要是说明控件的父窗口是谁

text = tk.Text(root, bg="#9EB34D", fg="white", font="迷你简小隶书")
text.insert(tk.END, "你好啊，我是text控件")
text.pack()

# 让窗体循环起来，窗体才会一直显示
root.mainloop()
```

![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2019-11-10_09-56-05.png "text控件属性")

```python
# Button控件
import tkinter as tk


def click():
    labelvar.set("我是Label控件呀")


# 生成一个Tk对象（也叫主窗体对象）
root = tk.Tk()

# 设置窗体的名称
root.title("GUI第一弹")

# 设置窗体的大小，中间的是小写的x
root.geometry("300x300")

root['background'] = "pink"

# 第一个参数主要是说明控件的父窗口是谁
# text属性是控件上面的文字
button = tk.Button(root, text="你好啊，我是Button控件", bg="orange", fg="white", command=click)
button.pack()

# 让窗体循环起来，窗体才会一直显示
root.mainloop()
```

![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2019-11-10_14-41-57.png "button属性")



```python
# label控件插入图片
from PIL import Image, ImageTk
import tkinter as tk

root = tk.Tk()

root.title("加载图片")
root.geometry("800x800+200+100")

img1 = Image.open("./爱心/7.jpg")
print(img1.size)
photo1 = ImageTk.PhotoImage(img1)

lb1 = tk.Label(root, image=photo1)
lb1.pack()

root.mainloop()
```

```python
# scale控件
import tkinter as tk

root = tk.Tk()


def show(a):
    # print(a)

    lb1.config(text="选择值:"+a)


root.title("scale 滑动块")
root.geometry("300x200+500+500")

sl1 = tk.Scale(root, orient=tk.HORIZONTAL, label="颜值", length=200, from_=30, to=60, tickinterval=5, command=show)
sl1.pack(anchor="w")

lb1 = tk.Label(root, text="选择值:")
lb1.pack(anchor="w")

root.mainloop()
```

![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2019-11-10_14-46-49.png "scale控件属性")



```python
# radiobutton单选框
import tkinter as tk

root = tk.Tk()


def showSelection():
    var.set(varR.get())


root.title("radioButton 单选框")
root.geometry("300x200+500+500")

varR = tk.StringVar()
# 不设置的话，默认选中三个，也可以设置其中某个的value值
varR.set(1)
# value用于显示的东西，通过command来绑定需要执行的函数,variable.get()得到的就是value中的内容
r1 = tk.Radiobutton(root, text="A、优酷", variable=varR, value="A、优酷", command=showSelection)
r1.pack(anchor="w")

r2 = tk.Radiobutton(root, text="B、爱奇艺", variable=varR, value="B、爱奇艺", command=showSelection)
r2.pack(anchor="w")

r3 = tk.Radiobutton(root, text="C、网易", variable=varR, value="C、网易", command=showSelection)
r3.pack(anchor="w")

label1 = tk.Label(root, text="所选的内容是:")
label1.pack(anchor="n", side="left")

var = tk.StringVar()
label2 = tk.Label(root, textvariable=var)
label2.pack(anchor="n", side="left")

root.mainloop()
```



![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2019-11-10_14-48-55.png "radiobutton控件属性")

```python
# checkbutton 复选框
import tkinter as tk

root = tk.Tk()

root.title("checkButton 复选框")
root.geometry("300x300+500+500")


def showSelection():
    str1 = ""
    if ck1var1.get() == 1:
        str1 += ck1.cget("text") + " "

    if ck1var2.get() == 1:
        str1 += ck2.cget("text") + " "

    if ck1var3.get() == 1:
        str1 += ck3.cget("text") + " "

    lblvar.set(str1)


ck1var1 = tk.IntVar()
ck1 = tk.Checkbutton(root, text="愿望一:小目标一个亿", onvalue=1, offvalue=0, variable=ck1var1, command=showSelection)
ck1.pack(anchor="w")

ck1var2 = tk.IntVar()
ck2 = tk.Checkbutton(root, text="愿望二:结婚吧", onvalue=1, offvalue=0, variable=ck1var2, command=showSelection)
ck2.pack(anchor="w")

ck1var3 = tk.IntVar()
ck3 = tk.Checkbutton(root, text="愿望三:慢慢变老", onvalue=1, offvalue=0, variable=ck1var3, command=showSelection)
ck3.pack(anchor="w")

lblvar = tk.StringVar()
lbl1 = tk.Label(root, textvariable=lblvar)
lbl1.pack(anchor="w")

root.mainloop()

```

![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2019-11-10_14-48-55.png "checkbutton复选框控件属性")

```python
# 屏幕居中
import tkinter as tk

window = tk.Tk()

window.title("屏幕居中")

# 求出屏幕的宽度和高度
sw = window.winfo_screenwidth()
sh = window.winfo_screenheight()

# 设置窗口的宽度和高度
ww = 400
wh = 300

x = (sw - ww) / 2
y = (sh - wh) / 2

window.geometry("%dx%d+%d+%d" % (ww, wh, x, y))

window.mainloop()
```

```python
# 滚动条关联text富文本框
import tkinter as tk

window = tk.Tk()

window.title("滚动条实例")
window.geometry("300x300+200+100")

scroll = tk.Scrollbar()
scroll.pack(side=tk.RIGHT, fill=tk.Y)

text = tk.Text(window)

text.insert(tk.INSERT, str)
text.pack(side=tk.LEFT, fill=tk.Y)

# 将滚动条和text相互绑定
scroll.config(command=text.yview)
text.config(yscrollcommand=scroll.set)


window.mainloop()
```

```python
# grid布局函数
import tkinter as tk

# 生成一个Tk对象（也叫主窗体对象）
root = tk.Tk()

# 设置窗体的名称
root.title("GUI第一弹")

# 设置窗体的大小，中间的是小写的x
root.geometry("300x300")

# root['background'] = "pink"

# 第一个参数主要是说明控件的父窗口是谁
# text属性是控件上面的文字
btn1 = tk.Button(root, text="btn1", fg="red", font="楷体", width=3, height=4)
btn1.grid(row=0, column=0, sticky="we")

btn2 = tk.Button(root, text="btn2", fg="blue", font="楷体")
btn2.grid(row=1, column=0, sticky="we")

# 让窗体循环起来，窗体才会一直显示
root.mainloop()

```

```python
# pack布局函数
import tkinter as tk

# 生成一个Tk对象（也叫主窗体对象）
root = tk.Tk()

# 设置窗体的名称
root.title("GUI第一弹")

# 设置窗体的大小，中间的是小写的x
root.geometry("300x300")

root['background'] = "pink"

# 第一个参数主要是说明控件的父窗口是谁
# text属性是控件上面的文字
label1 = tk.Label(root, text="你好啊，我是Label控件", bg="orange", fg="white", font="楷体")
label1.pack(anchor="w", ipadx=10, pady=10)

label2 = tk.Label(root, text="你好啊，我是Label控件", bg="orange", fg="white", font="楷体")
label2.pack(anchor="w", ipadx=10)

# 让窗体循环起来，窗体才会一直显示
root.mainloop()
```

```python
# place布局函数
import tkinter as tk

# 生成一个Tk对象（也叫主窗体对象）
root = tk.Tk()

# 设置窗体的名称
root.title("GUI第一弹")

# 设置窗体的大小，中间的是小写的x
root.geometry("300x300")

# root['background'] = "pink"

# 第一个参数主要是说明控件的父窗口是谁
# text属性是控件上面的文字
btn1 = tk.Button(root, text="btn1", fg="red", font="楷体")
btn1.place(x=0, y=0)

btn2 = tk.Button(root, text="btn2", fg="blue", font="楷体")
btn2.place(x=0, y=40)

# 让窗体循环起来，窗体才会一直显示
root.mainloop()
```

![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2019-11-10_14-56-29.png "布局函数参数")



```python
# menubar菜单栏
import tkinter as tk

root = tk.Tk()

root.title("menubar 菜单栏")
root.geometry("300x300+500+500")

menubar = tk.Menu(root)

def show():
    print("新建...")

filemenu = tk.Menu(menubar, tearoff=False)

filemenu.add_command(label="新建...", command=show)
filemenu.add_command(label="保存")
filemenu.add_command(label="另存...")
filemenu.add_command(label="退出")

# 添加分隔符
filemenu.add_separator()

svmenu = tk.Menu(filemenu, tearoff=False)
svmenu.add_command(label="收藏到本地")
svmenu.add_command(label="收藏到浏览器")


filemenu.add_cascade(label="收藏", menu=svmenu)
menubar.add_cascade(label="文件", menu=filemenu)

editmenu = tk.Menu(menubar, tearoff=False)
editmenu.add_command(label="撤销")
editmenu.add_command(label="复制")
editmenu.add_command(label="粘贴")
menubar.add_cascade(label="编辑", menu=editmenu)

menubar.add_cascade(label="作者", menu=filemenu)
menubar.add_cascade(label="帮助", menu=filemenu)

root.config(menu=menubar)
root.mainloop()

```



![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2019-11-10_18-45-06.png "菜单栏显示结果")

![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2019-11-10_18-47-38.png "菜单栏属性和方法")



**事件绑定**

![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2019-11-10_18-51-03.png "事件关联")

**鼠标事件**

![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2019-11-10_18-51-13.png"鼠标事件")



## 词云制作

```python
# 英文词云制作
import wordcloud

w = wordcloud.WordCloud()

w.generate('and that government of the people, by the people, for the people, shall not perish from the earth.')

w.to_file(r'C:\Users\Administrator\Desktop\file\日常学习\python学习笔记\词云制作\output1.png')
```

```python
# 中文词云制作，需要导入字体
import wordcloud

w = wordcloud.WordCloud(background_color='black',
                        height = 768,
                        width = 1366,
                        font_path='msyh.ttc')

w.generate('从明天起，做一个幸福的人。喂马、劈柴，周游世界。从明天起，关心粮食和蔬菜。我有一所房子，面朝大海，春暖花开')

w.to_file(r'C:\Users\Administrator\Desktop\file\日常学习\python学习笔记\词云制作\中文词云.png')
```

```
# wordcloud常见参数

width 词云图片宽度，默认400像素

height 词云图片高度 默认200像素

background_color 词云图片的背景颜色，默认为黑色

background_color='white'

font_step 字号增大的步进间隔 默认1号

font_path 指定字体路径 默认None，对于中文可用font_path='msyh.ttc'

mini_font_size 最小字号 默认4号

max_font_size 最大字号 根据高度自动调节

max_words 最大词数 默认200

stop_words 不显示的单词 stop_words={"python","java"}

Scale 默认值1。值越大，图像密度越大越清晰

prefer_horizontal：默认值0.90，浮点数类型。表示在水平如果不合适，就旋转为垂直方向，水平放置的词数占0.9？

relative_scaling：默认值0.5，浮点型。设定按词频倒序排列，上一个词相对下一位词的大小倍数。有如下取值：“0”表示大小标准只参考频率排名，“1”如果词频是2倍，大小也是2倍

mask 指定词云形状图片，默认为矩形

通过以下代码读入外部词云形状图片（需要先pip install imageio安装imageio）

import imageio
mk = imageio.imread("picture.png")
w = wordcloud.WordCloud(mask=mk)
```

```python
# 使用jieba库的lcut方法进行分词
import wordcloud
import os
import jieba

os.chdir(r'C:\Users\Administrator\Desktop\file\日常学习\python学习笔记\词云制作')

w = wordcloud.WordCloud(font_path='msyh.ttc',background_color='white',width=1366,height=768)

f = open('天津理工大学.txt',encoding = 'utf-8')
txt = f.read()

txt_list = jieba.lcut(txt)
txt_string = " ".join(txt_list)

w.generate(txt_string)

w.to_file('天津理工大学.png')
```

```python
# 替换蒙版，使用自己的图片进行词云制作
import wordcloud
import os
import jieba
import imageio

os.chdir(r'C:\Users\Administrator\Desktop\file\日常学习\python学习笔记\词云制作')

mk = imageio.imread('wujiaoxing.png')

w = wordcloud.WordCloud(font_path='msyh.ttc',
                        background_color='white',
                        width=1366,
                        height=768,
                        mask=mk,
                        scale=15)

f = open('关于实施乡村振兴战略的意见.txt',encoding = 'utf-8')
txt = f.read()

txt_list = jieba.lcut(txt)
txt_string = " ".join(txt_list)

w.generate(txt_string)

w.to_file('关于实施乡村振兴战略的意见_mask.png')
```

```python
# 设置停止词
import wordcloud
import os
import jieba
import imageio

os.chdir(r'C:\Users\86138\Desktop\日常学习\python学习笔记\词云制作')

mk = imageio.imread('chinamap.png')

w = wordcloud.WordCloud(font_path='msyh.ttc',
                        background_color='white',
                        width=1366,
                        height=768,
                        mask=mk,
                        scale=15,
                        stopwords={'曹操','孔明'})

f = open('三国演义.txt',encoding = 'utf-8')
txt = f.read()

txt_list = jieba.lcut(txt)
txt_string = " ".join(txt_list)

w.generate(txt_string)

w.to_file('三国演义.png')

```

```python
# 轮廓勾勒
import wordcloud
import os
import jieba
import imageio

os.chdir(r'C:\Users\Administrator\Desktop\file\日常学习\python学习笔记\词云制作')

mk = imageio.imread('alice.png')

w = wordcloud.WordCloud(
                        background_color='white',
                        mask=mk,
                        contour_width=1,
                        contour_color='steelblue'
)

f = open('hamlet.txt',encoding = 'utf-8')
txt = f.read()

txt_list = jieba.lcut(txt)
txt_string = " ".join(txt_list)

w.generate(txt_string)

w.to_file('哈姆雷特.png')
```

![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\哈姆雷特.png)

```python
# 模板上色
from wordcloud import WordCloud,ImageColorGenerator
import os
import jieba
import imageio

os.chdir(r'C:\Users\Administrator\Desktop\file\日常学习\python学习笔记\词云制作')

mk = imageio.imread('alice_color.png')
imgcolor = ImageColorGenerator(mk)

w = WordCloud(
                        background_color='white',
                        mask=mk
)

f = open('hamlet.txt',encoding = 'utf-8')
txt = f.read()

txt_list = jieba.lcut(txt)
txt_string = " ".join(txt_list)

w.generate(txt_string)
w_color = w.recolor(color_func = imgcolor)

w_color.to_file('哈姆雷特2.png')
```

![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\哈姆雷特2.png)



## concurrent模块

+  **从Python3.2开始**，标准库为我们提供了**concurrent.futures**模块，它提供了**ThreadPoolExecutor**和**ProcessPoolExecutor**两个类，实现了对**threading**和**multiprocessing**的进一步抽象，对编写线程池/进程池提供了直接的支持。 

```python
# 线程池
def load_url(url):
    with urllib.request.urlopen(url, timeout=60) as conn:
        print('%r page is %d bytes' % (url, len(conn.read())))

executor = ThreadPoolExecutor(max_workers=3)

for url in URLS:
    future = executor.submit(load_url,url)
    print(future.done())
# 运行结果：
False
False
False
主线程
'https://www.baidu.com/' page is 227 bytes
'http://www.163.com' page is 662047 bytes
'https://github.com/' page is 54629 bytes
```

+  我们使用**submit**方法来往线程池中加入一个**task**，submit返回一个**Future对象**，对于Future对象可以简单地理解为一个在**未来完成的操作**。由于**线程池异步提交了任务**，**主线程并不会等待线程池里创建的线程执行完毕**，所以执行了print('主线程')，相应的线程池中创建的线程并没有执行完毕，故future.done()返回结果为False。 

+ 进程池代码同上

+ ```python
  # 进程池
  def load_url(url):
      with urllib.request.urlopen(url, timeout=60) as conn:
          print('%r page is %d bytes' % (url, len(conn.read())))
  
  executor = ProcessPoolExecutor(max_workers=3)
  
  for url in URLS:
      future = executor.submit(load_url,url)
      print(future.done())
  # 运行结果：
  False
  False
  False
  主线程
  'https://www.baidu.com/' page is 227 bytes
  'http://www.163.com' page is 662047 bytes
  'https://github.com/' page is 54629 bytes
  ```

+ ### **使用map来操作线程池/进程池**

  + ```python
    from concurrent.futures import ThreadPoolExecutor
    import urllib.request
    URLS = ['http://www.163.com', 'https://www.baidu.com/', 'https://github.com/']
    def load_url(url):
        with urllib.request.urlopen(url, timeout=60) as conn:
            print('%r page is %d bytes' % (url, len(conn.read())))
    
    executor = ThreadPoolExecutor(max_workers=3)
    
    executor.map(load_url,URLS)
    
    print('主线程')
    
    # 运行结果：
    主线程
    'http://www.163.com' page is 662047 bytes
    'https://www.baidu.com/' page is 227 bytes
    'https://github.com/' page is 54629 bytes
    ```

## schedule 定时任务

+ ```python
  import schedule
  import time
  
  
  def job():
      print("I'm working...")
  
  
  schedule.every(10).minutes.do(job)
  schedule.every().hour.do(job)
  schedule.every().day.at("10:30").do(job)
  schedule.every(5).to(10).days.do(job)
  schedule.every().monday.do(job)
  schedule.every().wednesday.at("13:15").do(job)
  
  
  while True:
      schedule.run_pending()
      time.sleep(1)
  
  
      
  """
  上面的大致意思：
  每隔十分钟执行一次任务
  每隔一小时执行一次任务
  每天的10:30执行一次任务
  每隔5到10天执行一次任务 
  每周一的这个时候执行一次任务
  每周三13:15执行一次任务
  run_pending：运行所有可以运行的任务
  """
  ```

## PEP8 代码规范

### 代码布局

+ 缩进

  + 每一级缩进使用4个空格

  + 推荐写法

    + ```python
      # 与左括号对齐
      foo = long_function_name(var_one, var_two,
                               var_three, var_four)
      
      # 用更多的缩进来与其他行区分
      def long_function_name(
              var_one, var_two, var_three,
              var_four):
          print(var_one)
      
      # 挂行缩进应该再换一行
      foo = long_function_name(
          var_one, var_two,
          var_three, var_four)
      ```

  + 不推荐写法

    + ```python
      # 没有使用垂直对齐时，禁止把参数放在第一行
      foo = long_function_name(var_one, var_two,
          var_three, var_four)
      
      # 当缩进没有与其他行区分时，要增加缩进
      def long_function_name(
          var_one, var_two, var_three,
          var_four):
          print(var_one)
      ```

  + if语句条件过长

    + ```python
      # 没有额外的缩进
      if (this_is_one_thing and
          that_is_another_thing):
          do_something()
      
      # 增加一个注释，在能提供语法高亮的编辑器中可以有一些区分
      if (this_is_one_thing and
          that_is_another_thing):
          # Since both conditions are true, we can frobnicate.
          do_something()
      
      # 在条件判断的语句添加额外的缩进
      if (this_is_one_thing
              and that_is_another_thing):
          do_something()
      ```

  + 括号问题

    + ```python
      my_list = [
          1, 2, 3,
          4, 5, 6,
          ]
      result = some_function_that_takes_arguments(
          'a', 'b', 'c',
          'd', 'e', 'f',
          )
      ```

    + ```python
      my_list = [
          1, 2, 3,
          4, 5, 6,
      ]
      result = some_function_that_takes_arguments(
          'a', 'b', 'c',
          'd', 'e', 'f',
      )
      ```

+ **空行问题**
  + **顶层函数和类的定义**，前后使用**两个空行**隔开
  + **类里面的方法定义**使用**一个空行**隔开

+ **表达式和语句中的空格**

  + 紧跟在小括号，中括号或者大括号后

    + ```
      Yes: spam(ham[1], {eggs: 2})
      No:  spam( ham[ 1 ], { eggs: 2 } )
      ```

  + 紧贴在逗号、分号或者冒号之前

    + ```
      Yes: if x == 4: print x, y; x, y = y, x
      No: if x == 4 : print x , y ; x , y = y , x
      ```

  + 在切片操作中，冒号前后必须有相同的间距

  + 紧贴在函数参数的左括号之前

    + ```
      Yes: spam(1)
      No: spam (1)
      ```

  + 紧贴索引或者切片的左括号之前

    + ```
      Yes: dct['key'] = lst[index]
      No: dct ['key'] = lst [index]
      ```

  +  为了和另一个赋值语句对齐，在赋值运算符附件加多个空格。  

    + 推荐

      ```
      x = 1
      y = 2
      long_variable = 3
      ```

    + 不推荐

      ```
      x             = 1
      y             = 2
      long_variable = 3
      ```

  + 其他建议

    + 推荐

      ```
      i = i + 1
      submitted += 1
      x = x*2 - 1
      hypot2 = x*x + y*y
      c = (a+b) * (a-b)
      ```

    + 不推荐

      ```
      i=i+1
      submitted +=1
      x = x * 2 - 1
      hypot2 = x * x + y * y
      c = (a + b) * (a - b)
      ```

  + 在制定关键字参数或者默认参数的时候，不要在=附近加上空格

    + 推荐

      ```
      def complex(real, imag=0.0):
          return magic(r=real, i=imag)
      ```

+ doc string

  + ```python
    """Return a foobang
    
    Optional plotz says to frobnicate the bizbaz first.
    """
    ```

+ 命名规范 name conventions

  + 最重要的原则
    + 那些暴露给用户的API接口的命名，应该遵循反映使用场景而不是实现的原则

  + 命名风格

    + b (单个小写字母)
    + B (单个大写字母)
    + lowercase 小写字母
    + lower_case_with_underscores 使用下划线分隔的小写字母
    + UPPERCASE 大写字母

    + UPPER_CASE_WITH_UNDERSCORES 使用下划线分隔的大写字母
    + CapWords 驼峰命名法
      + 当在首字母大写的风格中使用到缩写时，所有缩写的字母用大写，因此HTTPServerError 比HttpServerError要好

  + 包名和模块名
    + 模块应该用简短全小写的名字，如果为了提升可读性，下划线也是可以用的
    + 包名亦如此

  + 类名
    + 一般使用首字母大写的约定

## python Tips

#### import搜索路径

+  

  ```
  import sys
  
  sys.path
  ```

+ 返回值是一个列表，搜索的路径在这个列表中

+ **导入模块，最好从上一级目录开始写**

+ **python会先搜索当前目录**

+ **然后搜索系统目录**

+ ```
  __file__
  可以显示当前导入模块的完整路径
  ```

+ sys.path.insert(0, path)
  + 这样就可以把你的路径添加到第一个位置
  + python会按照顺序进行搜索

#### == and is

+ **==** 判断**内容**是否相同
+ **is** 判断是否是同一个**对象**

#### 取商和余数

+ divmod(10, 3)
+ (3, 1)

#### print函数

+ print默认的是在最后**加入换行符**，如果想要改变，只需在**print(item,)**，这样就可以了，python会默认的**加上一个空格**，以便美观

#### 将str当成有效表达式来求值，并返回运算结果

+ ```
  s = "1 + 3 + 5"
  eval(s)
  out : 9
  ```

  

#### enumerate()函数

+ ```python
  for i, ch in enumerate(foo):
  	print(ch, "(%d)" % i)
  
  """
  运行结果:
  a (0)
  b (1)
  c (2)
  """
  ```



------

updated in 2019年11月22日08:21:09

#### 列表解析式

------



+ **[expr for iter_var in iterable]**

  + ```python
    s = [x**2 for x in range(4)]
    
    for i in s:
        print(i)
    ```

  + **map(lambda x:x**2,  range(4))

+ **[expr for iter_var in iterable if cond_expr]**

  + 可以用来过滤满足条件表达式cond_expr的序列成员
  + **filter(lambda x:x%2, seq)**
    + 当 x%2 == 1的时候，通过，过滤掉偶数，留下奇数



#### 三元表达式

```python
smaller = x if x<y else y
```

#### xrange 内建函数

------



+ 和range非常类似，只是当数据量过大时，可以使用xrange,因为它**不会在内存中生成一个完整的拷贝**，所以在未来，range函数可能被xrange替代

#### 与序列相关的内建函数

------



+ sorted

+ reversed

+ enumerate

  + ```python
    for i, album in enumerate(albums):
    	print(i, album)
    
    ................................
    0 poe
    1 Gaudi
    2 Freud
    3 Poe2
    ```

+ zip

  + ```python
    for album, yr in zip(albums, years):
    	print(yr, album)
    ..................................
    1976 Poe
    1987 Gaudi
    1990 Freud
    ```



#### 可迭代对象、迭代器和生成器的区别

------

![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2019-11-22_08-32-01.png "三者关系")可迭代对象和迭代器

+ 可迭代对象包含迭代器
+ 如果一个对象拥有**_iter_**方法，是**可迭代对象**；如果一个对象拥有**next方法**，是**迭代器**
+ 定义可迭代对象，必须拥有_iter_方法；定义迭代器必须实现_iter_和next方法

**生成器**

+ **特殊的迭代器**
+ list [i*2 for i in range(5)]
+ generator (i*2 for i in range(5))
+ 如果函数中有**yield关键字**，那么这个函数就变成了**生成器**
+ yield关键字可以使得函数执行暂停，**类似于return**，下次从这个地方继续执行。
+ **节省空间**



#### for循环和else结合使用

------

```python
for i in range(10):
    if i == 5:
        print 'found it! i = %s' % i
else:
    print 'not found it ...'

 ........................................
found it!i = 5
not found it
```

+ for循环结束的时候会执行else语句，不想执行的话，可以加上break语句，这样就可以跳过去不执行了

#### pprint模块

------

+ 常常使用pprint.pprint函数来打印字典或者json格式的数据，比较好看规整
+ 其他打印的结果和print函数显示的效果一样

#### 全局变量修改问题

------

+ **不是所有**的情况都需要加**global**
+ 只要这个变量的**指向没有变**，就不需要使用global
+ 除非指向发生了变化

## pickle模块

### 内存中操作

```python
import pickle
#dumps
li = [11,22,33]
r = pickle.dumps(li)
print(r)


#loads
result = pickle.loads(r)
print(result)
```

### 文本中操作

```python
#dump：
li = [11,22,33]
pickle.dump(li,open('db','wb'))

#load
ret = pickle.load(open('db','rb'))
print(ret)
```

## 常见数据类型的转换



## pip指令

### 升级所有模块

+ ```
  pip install pip-review
  pip-review --local --interactive
  ```

### 安装包

+ ```
  pip install packagename # 最新版本
  pip install packagename==1.0.4 # 指定版本
  pip install -r requirements.txt
  ```

### 升级包

+ ```
  pip install -U packagename
  pip install --upgrade packagename
  pip install --upgrade package_name
  ```

### 升级pip

+ ```
  pip install -U pip
  python -m pip install --upgrade pip
  ```

### 查看已经安装的包及版本信息

+ ```
  pip freeze
  ```

### 生成requirements.txt文件

+ ```
  pip freeze > path\requirements.txt
  ```

### 查看可升级的包

+ ```
  pip list -o
  ```

### 显示包及所在目录

+ ```
  pip show packagename
  ```

## python进阶

+ `collections工具类`

  + ```python
    """
    找出序列中出现次数最多的元素
    """
    from collections import Counter
    
    words = [
        'look', 'into', 'my', 'eyes', 'look', 'into', 'my', 'eyes',
        'the', 'eyes', 'the', 'eyes', 'the', 'eyes', 'not', 'around',
        'the', 'eyes', "don't", 'look', 'around', 'the', 'eyes',
        'look', 'into', 'my', 'eyes', "you're", 'under'
    ]
    counter = Counter(words)
    print(counter.most_common(3))
    ```

+ 函数的使用方式
  + 将函数视为‘一等公民’
    + 函数可以赋值给变量
    + 函数可以作为函数的参数
    + 函数可以作为函数的返回值

+ 生成器

  + ⾸先我们要理解`迭代器(iterators)`。根据维基百科，`迭代器`是⼀个让程序员`可以遍历`⼀个容器（特别是列表）的对象。然⽽，⼀个迭代器在遍历并读取⼀个容器的数据元素时，并不会执⾏⼀个迭代。你可能有点晕了，那我们来个慢动作。换句话说这⾥有三个部分
    + `可迭代对象`
      + 只要定义了可以返回一个迭代器的**iter**方法。或者定义了支持下标索引的getitem方法
    + `迭代器`
      + 定义了一个**next**方法
      + 可以使用**iter**这个内置方法，将可迭代对象变成一个迭代器
+ 生成器也是一种迭代器，但是只能迭代一次。含有**yield**关键字
  
+ **最佳应用场景**：不想同一时间将所有计算出来的结果都加载到内存当中，特别是结果还包含循环.
  
+ **虚拟环境(virtualenv)**

  + `概念`
    + 是一个工具，可以帮助我们创建一个独立的python环境

  + `使用场景`
    + 有一个应用程序依赖于版本2的第三方模块，有一个程序依赖于版本3的模块
    + 已经开发好了一个程序，但是不想更新它所依赖的第三方模块，但是你已经开始另一个程序，需要这些第三方模块的版本

  + `安装`
    + pip install virtualenv

  + `常用指令`

    + virtualenv myproject
      + 创建一个隔离的virtualenv环境

    + virtualenv myproject `--no-site-packages`
      + 安装到python环境中的所有第三方包都不会复制过来

    + source bin/activate
      + 激活隔离的环境

    + deactivate
      + 退出这个virtualenv,进而可以使用系统全局的python模块

  + **注**：
    + 默认情况下,virtualenv不会使用系统全局模块
    + 如果想要让你的virtualenv使用系统全局模块，请使用--system-site-packages参数创建你的virtualenv

+ **对象自省(introspection)**

  + `dir`
    + 它返回的是一个列表，列出了这个对象所有的属性和方法
+ `type`
  
+ `id`
  
+ **推导式**

  + `定义`
    + 又称解析式，是python独有的一种特性，他可以从一个数据序列创建另一个新的数据序列的结构体

  + `分类`
    + 列表推导式
      + variable = [out_exp  for out_exp in input_list if out_exp]
    + 字典推导式
      + {v:k for v,k in some_dict.items()}
    + 集合推导式
      + 跟列表推导式一样，唯一不同的是把中括号换成了大括号

## Ubuntu 开发

+ **常用命令**
  + 输出系统环境变量
    + `echo $PATH`
  
+ **安装pip**
  
  + `sudo apt install python(3)-pip`
  
+ **设置pip安装源（~/.pip/pip.config）**
  + `[global]`
    `trusted-host =  pypi.douban.com`
    `index-url = http://pypi.douban.com/simple`
  
+ **安装pycharm**
  + `下载tar.gz安装包`
  + `tar xzvf py......`
  + `cd .../bin`
  + `./pycharm.sh 启动`
  
+ **查看python安装路径**
  
  + `which python`
  
+ **查看python版本**
  
  + `python --version`
  
+ **py2 -> py3**
  + 打开terminal
  + sudo vi ~/.bashrc
  + 添加 alias python='python3'
  + source ~/.bashrc

+ **设置root用户密码**
  
+ `sudo passwd`
  
+ virtualenv的创建、使用和管理

  + 创建
    + pip install virtualenv
    + virtualenv venv  就会创建一个文件夹，这个文件夹就是一个独立的环境
    + 可以使用 -p python_path来指定python版本的解释器

  + 使用
    + source venv/bin/activate  激活当前环境
    + deactivate  退出当前环境

  + 常用参数

    + ```
      –version
      显示当前版本号。
      -h, –help
      显示帮助信息。
      -v, –verbose
      显示详细信息。
      -q, –quiet
      不显示详细信息。
      -p PYTHON_EXE, –python=PYTHON_EXE
      指定所用的python解析器的版本，比如 –python=python2.5 就使用2.5版本的解析器创建新的隔离环境。 默认使用的是当前系统安装(/usr/bin/python)的python解析器
      –clear
      清空非root用户的安装，并重头开始创建隔离环境。
      –no-site-packages
      令隔离环境不能访问系统全局的site-packages目录。
      –system-site-packages
      令隔离环境可以访问系统全局的site-packages目录。
      –unzip-setuptools
      安装时解压Setuptools或Distribute
      –relocatable
      重定位某个已存在的隔离环境。使用该选项将修正脚本并令所有.pth文件使用相当路径。
      –distribute
      使用Distribute代替Setuptools，也可设置环境变量VIRTUALENV_DISTRIBUTE达到同样效要。
      –extra-search-dir=SEARCH_DIRS
      用于查找setuptools/distribute/pip发布包的目录。可以添加任意数量的–extra-search-dir路径。
      –never-download
      禁止从网上下载任何数据。此时，如果在本地搜索发布包失败，virtualenv就会报错。
      –prompt==PROMPT
      定义隔离环境的命令行前缀。
      ```

+ wrapper的使用

  + 首先配置一个系统变量WORKON_HOME，以后所有的环境都会安装到此环境下
  + `创建虚拟环境`
    + mkvirtualenv 虚拟环境名称
  + `指定python版本`
    + -p python
  
  + `workon env`
    + 进入环境
  + `deactivate` 
    + 离开环境
  + `rmvirtualenv spider`
    + 删除环境  

## 多任务

+ **并行**：`真`的多任务
+ **并发**：`假`的多任务
+ **threading模块**
  + threading.Thread()
    + 创建一个子线程
  + threading.enumerate()
    + 返回正在执行的线程

+ **线程同步**
  + 要么不做，要么做完
  + **互斥锁**
    + threading.Lock()
    + lk.require()    # 上锁
    + lk.release()    # 开锁

+ **进程**

  + `定义`
    + 是资源分配的基本单位，程序运行起来之后，用到的资源称之为进程

  + `状态`
    + 就绪
    + 运行
    + 等待
    + 死亡

  + `创建`
    + from multiprocessing import Process  其余类似于多线程

  + `缺点`
    + **耗费的资源太多**，子进程和主进程的资源一样，除了pid不一样，所以耗费的东西很多。

+ **进程和线程的区别**
  + 多进程，相当于在一个电脑中运行多个QQ，资源分配的单位，`进程之间互相独立`
  + 多线程，相当于一个QQ多个聊天窗口，资源调度的单位，线程之间共享全局变量

+ **进程之间的通信**
  + from multiprocessing import Queue
  + q.put()
  + q.get()
  + q.empty()
  + q.full()

+ **进程池pool**
  + 不知道需要创建多少个进程的时候
  + 进程数太多的时候

## 发送邮件

```python
import smtplib
from email.mime.text import MIMEText
from email.header import Header


def sendemail(data):
    # 第三方 SMTP 服务
    mail_host = "smtp.163.com"  # 设置服务器
    mail_user = "m13821003591_1" # 用户名
    mail_pass = "138210wwc"  # 口令

    sender = '13821003591@163.com'
    receiver = '1578495112@qq.com'  # 接收邮件，可设置为你的QQ邮箱或者其他邮箱

    message = MIMEText(data, 'plain', 'utf-8')
    message['From'] = '<13821003591@163.com>'
    message['To'] = '<1578495112@qq.com>'

    subject = '新型冠状病毒最新数据'
    message['Subject'] = Header(subject, 'utf-8')

    try:
        smtpObj = smtplib.SMTP()
        smtpObj.connect(mail_host, 25)
        smtpObj.login(mail_user, mail_pass)
        smtpObj.sendmail(sender, receiver, message.as_string())
        print("邮件发送成功")
    except Exception as e:
        print("Error: 无法发送邮件:{}".format(e))


if __name__ == '__main__':
    sendemail('你还好么')
```

```python
# 带有附件
def send_multimail(data):
    """带有附件的邮件发送"""
    # 创建一个带附件的实例
    message = MIMEMultipart()
    message['From'] = '<13821003591@163.com>'
    message['To'] = '<1578495112@qq.com>'
    subject = 'Python SMTP 邮件'
    message['Subject'] = Header(subject, 'utf-8')

    # 邮件正文内容
    message.attach(MIMEText(data, 'plain', 'utf-8'))

    # 构造附件1，传送当前目录下的 test.txt 文件
    att1 = MIMEText(open('data.txt', 'rb').read(), 'base64', 'utf-8')
    att1["Content-Type"] = 'application/octet-stream'
    # 这里的filename可以任意写，写什么名字，邮件中显示什么名字
    att1.add_header("Content-Disposition", 'attachment', filename="冠状病毒数据.txt")
    message.attach(att1)

    try:
        smtpObj = smtplib.SMTP()
        smtpObj.connect(mail_host, 25)
        smtpObj.login(mail_user, mail_pass)
        smtpObj.sendmail(sender, receiver, message.as_string())
        print("邮件发送成功")
    except Exception as e:
        print("Error: 无法发送邮件:{}".format(e))

```

## pycharm常用快捷键

+ alt+< 源码和本码之间切换
+ alt+>