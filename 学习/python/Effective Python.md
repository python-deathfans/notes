# 第一章 用pythonic方式来思考

## 第一条 遵循PEP8风格指南

+ **函数、变量及属性**应该用**小写字母**来拼写，各单词之间以**下划线**相连， lowercase_underscore
+ **受保护的属性**应该以**单下划线**开头
+ **私有属性**应该以**两个下划线**开头
+ 类名遵从**大驼峰**命名方式，函数名遵从**小驼峰**命名
+ 在使用**下标来获取列表元素**、**调用函数**或给**关键字参数赋值**的时候，**不要在两旁添加空格**。
+ **变量赋值**的时候需要在**两侧添加一个空格**
+ 类与异常，应该用每个单词首字母大写的形式来命名，例如CapitalizedWord
+ **表达式语句**：
  - [ ] 采用内联形式的否定词，例如if a is not b
  - [ ] 如果想要**判断是否为空**，应该使用**if not somelist**
  - [ ] 如果**判断是否是非空**，应该使用**if somelist**
  - [ ] 引入模块的时候，总是使用绝对名称，而不应该使用相对路径
  - [ ] 如果想要使用相对路径，**from . import foo**

## 第二条 了解bytes、str、与unicode的区别

​		python3有两种表示字符序列的类型：**bytes和str**。前者的实例包含原始的8位值，后者的实例包含**Unicode字符**。

​		把Unicode字符表示为2进制数据（也就是原始8位值）有许多方法。**最常见的编码方式是UTF-8**。但大家要记住Python3的str实例和python2的unicode实例都没有和特定的二进制编码形式相关联。要想把Unicode字符转换成二进制数据，必须使用**encode**方法。要想把二进制数据转换成Unicode字符，必须使用**decode**方法。

​		由于字符类型有别，所以Python代码中经常会出现两种常见的使用情景：

- [ ] 开发者需要原始8位值，这些8位值以UTF-8格式来编码的字符

- [ ] 开发者需要操作没有特定编码格式的Unicode字符

  ​	所以我们需要编写两个辅助(helper)函数，以便在这两种情况之间转换，使得转换之后的输入数据符合开发者的预期。

## 第三条 用列表推导来取代map和filter

+ 列表推导式

  + ```python
    a = [1, 3, 4325, 5, 45, 546, 56]
    b = [x**2 for x in a if a>4]
    ```

   + 上面的式子完成了map和filter的工作

   + 推荐使用上面的方法，其他的不推荐

   + 简洁明了

   + 其他结构也是支持推导式的

## 第四条 用生成器表达式来改写数据量较大的列表推导

> 列表推导的缺点：在推导过程中，对于输入的每个值，都需要去开辟内存，数据量小的情况下还好，数据量很大的时候，程序可能出现崩坏，这个时候生成器表达式应运而生

+ 把实现列表推导所用的那种写法放在一对**圆括号**中，就构成了**生成器表达式**

+ 注：
  + 当输入的数据量很大的时候，**列表推导可能会占用太多的内存而出问题**
  + 把某个生成器表达式所返回的迭代器，放在另一个生成器表达式的for子句中，可以组合使用
  + 穿在一起的生成器表达式的执行速度很快

## 第五条 尽量使用enumerate代替range

+ enumerate函数提供了一种精简的写法，可以在遍历迭代器时获知每个元素的索引
+ 可以给enumerate函数提供第二个参数，以指定开始计数时所用的值(默认为0)

## 第六条 zip函数可以同时遍历两个迭代器

+ 内置的zip函数可以平行地遍历多个迭代器
+ python3中的zip相当于生成器，会在遍历过程中主次产生元组
+ 如果提供的迭代器长度不等，那么zip就会提前终止
+ itertools内置模块中的zip_longest函数可以平行遍历多个迭代器，而不用在乎他们的长度是否相等 

## 第七条 合理利用try/except/else/finally

+ **finally**,顾名思义，不管发布发生异常，最后都会执行

  + ```python
    handle = open('test.txt') # May raise IOError
    try:
    	data = handle.read()	# May raise UnicodeDecodeError
    finally:
    	handle.close()		# Always runs after try
    ```

+ **else**.如果try块没有发生异常，那么执行else块，我们可以尽量**缩减try块内的代码量**。

  + ```python
    def load_json_key(data, key):
    	try:
    		result_dict = json.loads(data)	# May raise ValueError
        except ValueError as e:
        	raise KeyError from e
        else:
        	return result_dict[key]	# May raise KeyError
    ```

+ **混合使用**。我们可以使用**try**块来**读取文件并处理内容**，用**except**块来应对try块中可能发生的**相关异常**，用**else**块实时地**更新文件并把更新中可能出现的异常汇报给上级代码**，最后**finally**块来**清理文件句柄**。

# 第二章 函数

## 第七条 考虑用生成器来改写直接返回列表的函数

+ 生成器是使用yield表达式的函数
+ 调用生成器函数时，它不会真的运行，而是返回迭代器
+ 每次在迭代器上面调用内置的next函数时，迭代器会把生成器推进到下一个yield表达式那里
+ 可以把yield看成return，但是还是有点区别
+ 无论输入量有多大，生成器都能产生一系列输出，因为输入量和输出量，都不会影响它在执行时所耗的内存

## 第八条 在参数迭代时，要多加小心

+ 函数在输入的参数上面多次迭代时要当心；如果参数是迭代器，那么可能会导致奇怪的行为并错失某些值
+ python的迭代器协议，描述了容器和迭代器应该如何与iter和next内置函数，for循环及相关表达式相互配合。