# 第一章 模式匹配与正则表达式

## 1.1 用正则表达式查找文本模式

### 1.1.1 创建正则表达式对象

```python
"""
学习如何创建正则表达式
2020年3月4日19:08:11
\d 表示匹配任意一个数字
{} 表示匹配几次
search函数返回的对象有group函数，返回匹配结果
"""

import re

phoneNumberRegex = re.compile(r'\d{3}_\d{3}_\d{4}')

mo = phoneNumberRegex.search('My Number is 312_345_5454')

print(mo.group())
```

+ 总结
  + 使用import re导入正则表达式模块
  + 用re.compile()函数创建一个Regex对象
  + 向Regex对象的search()方法传入想要查找的字符串，返回Match对象
  + 调用Match对象的group方法，返回匹配文本的字符串

### 1.1.2 使用括号分组

```python
"""
学习使用括号分组
2020-3-4 19:16:24
"""

import re

phoneNumberRegex = re.compile(r'(\d{3})-(\d{3})-(\d{4})')

mo = phoneNumberRegex.search("my number is 123-345-5646")

print(mo.group(1))
print(type(mo.group()))
```

### 1.1.3 ?实现可选匹配

```python
"""
有的时候匹配的模式是可选的
字符?表面他前面的分组在这个模式中是可可选的
也可以说?前面的模式匹配了0次或者1次
2020年3月4日19:25:55
"""

import re

batRex = re.compile(r'Bat(wo)?man')

mo1 = batRex.search('The Adventure of Batman')
mo2 = batRex.search('The Adventure of Batwoman')

print(mo1.group())
print(mo2.group())
```

### 1.1.4 *实现任意次匹配

```python
"""
*意味着“匹配零次或者多次”
即星号之前的模式可以出现任意次
"""

import re

batRex = re.compile(r'Bat(wo)*man')

mo1 = batRex.search('The Adventure of Batman')
mo2 = batRex.search('The Adventure of Batwoman')
mo3 = batRex.search('The Adventure of Batwowowowowoman')

print(mo1.group())
print(mo2.group())
print(mo3.group())
```

### 1.1.5 +表示匹配1次或者多次

+ +号前面的模式至少出现一次

### 1.1.6 {}匹配特定的次数

+ {3}  匹配3次
+ {，3}   至多匹配3次
+ {3, 5}    匹配3到5次

### 1.1.7 贪心匹配和非贪心匹配

+ ```python
  """
  python默认的是贪心匹配
  如果加上?表示的就是非贪心匹配
  返回的是匹配最短的结果
  2020年3月5日17:07:02
  """
  
  import re
  
  greedyRex = re.compile(r'(Ha){3,5}')
  ingreedyRex = re.compile(r'(Ha){3,5}?')
  
  mo1 = greedyRex.search('HaHaHaHaHaHa')
  mo2 = ingreedyRex.search('HaHaHaHaHaHa')
  
  print(mo1.group())
  print(mo2.group())
  
  ```

### 1.1.8 findall方法

+ ```python
  """
  search方法只返回第一个匹配的结果
  findall方法返回的是匹配的所有结果
  返回结果是一个字符列表
  """
  
  import re
  
  greedyRex = re.compile(r'(Ha){3,5}')
  ingreedyRex = re.compile(r'(Ha){3,5}?')
  
  mo1 = greedyRex.findall('HaHaHaHaHaHa')
  mo2 = ingreedyRex.findall('HaHaHaHaHaHa')
  
  print(mo1)
  print(mo2)
  
  ```

# 第二章 操作excel表格

