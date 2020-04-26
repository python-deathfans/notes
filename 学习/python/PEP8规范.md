## indentation

+ ```python
  # Aligned with opening delimiter.
  foo = long_function_name(var_one, var_two,
                           var_three, var_four)
  
  # Add 4 spaces (an extra level of indentation) to distinguish arguments from the rest.
  def long_function_name(
          var_one, var_two, var_three,
          var_four):
      print(var_one)
  
  # Hanging indents should add a level.
  foo = long_function_name(
      var_one, var_two,
      var_three, var_four)
  ```

## 空格的使用

1. 使用空`格来表示缩进`，不要使用Tab

2. 和语法相关的每一层都要用4个空格进行表示

3. 每行的字符数不要超过`79`个

4. `函数和类`的定义，代码前后都要用`两个空行`进行分割

5. `同一个类`中，各个方法之间使用`一个空行`进行分隔

6. 一下情况避免使用多余的空行

   ```
   # 紧挨着小括号，中括号，大括号
   Yes: spam(ham[1], {eggs: 2})
   No: spam(ham[ 1 ], { eggs: 2 })
   
   # 紧挨着逗号， 分号， 冒号前
   Yes: if x == 4: print(x, y); x, y = y, x
   No: if x == 4 : print(x , y) ; x ,y = y , x
   ```

   



## 标识符命名

+ 变量、函数和属性应该使用小写字母来拼写，如果有多个单词就使用下划线进行连接
+ 类中受`保护`的实例属性，应该你使用`一个下划线`开头
+ 类中`私有`的实例属性，应该以`两个下划线`开头
+ 类和异常的命名，应该每个单词首字母进行大写



## 表达式和语句

+ 采用内联形式的否定词，而不要把否定词放在整个表达式的前面。例如 `if a is not b` 就比 `if not a is b` 更容易让人理解
+ 不要用检查长度的方式来判断字符串、列表等`是否是None或没有元素`，应该用 `if not x` 这样的写法来检查它。
+ import 语句总是在文件开头的地方
+ 引入模块的时候， from math import sqrt 比 import math 更好
+ 如果有多个import 语句，应该将其分为三部分，从上到下分别是Pyrthon标准模块、第三方模块和自定义模块，每个部分内部应该按照字母表的顺序来排列。