## shell编程快速入门

+ **内容**
  + **脚本声明**
    + 告知系统用何种shell来解释 **#!**
  + **注释信息**
    + 对执行程序进行介绍说明，可以不写 **#**
  + **可执行语句**
    + 执行的具体命令
+ **格式要求**
  + 脚本以**# !/bin/bash** 开头
  + 脚本需要有可执行权限
  + **一般后缀是sh**
+ **实例演示**
  + 创建脚本，输出hello world
+ **运行方式**
  + (输入绝对路径或者相对路径)
    + 赋予文件x权限
      + chmod 744 myshell.sh
    + 执行脚本
      + 相对路径
      + 绝对路径
  + (sh + 脚本) `不推荐`

## 接受用户的参数

+ SHELL脚本为了能够让用户灵活的完成工作需求，应该有办法接收用户输入的参数，像上面的脚本的写法真的很不灵活。
+ <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-21_07-22-42.png" style="zoom:80%;" />

+ SHELL**预定义变量**
  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-21_07-23-38.png" style="zoom:80%;" />

## 判断用户的参数

+ SHELL脚本有时还要判断用户输入的参数，例如像**mkdir**命令一样，当目录不存在则创建，若已经存在则报错，**条件测试语句能够测试特定的表达式是否成立，当条件成立时返回值为0，否则返回其他数值**。

+ <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-21_07-34-22.png" style="zoom:80%;" />

+ <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-21_07-35-00.png" style="zoom:80%;" />

+ 整数值比较: [ 整数1 操作符 整数2 ]

  + | 操作符 | 作用               |
    | ------ | ------------------ |
    | -eq    | 判断是否相等       |
    | -ne    | 判断是否不大于     |
    | -gt    | 判断是否大于       |
    | -lt    | 判断是否小于       |
    | -le    | 判断是否等于或小于 |
    | -ge    | 判断是否大于或等于 |

## 条件测试语句

+ if条件语句
  + 单分支结构
    + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-22_08-30-02.png" style="zoom:80%;" />
  + 双分支结构
    + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-22_08-31-34.png" style="zoom:80%;" />
  + 多分支结构
    + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-22_08-33-11.png" style="zoom:67%;" />

## shell的变量

+ **分类**
  + **系统变量**
  + **自定义变量**
+ **定义规则**
  + 变量名不能以数字开头
  + **等号两边不能有空格**
  + 变**量名一般为大写**
  + 赋值
    + a = $(b)
    + a = `b`(反引号)
+ **系统变量**
  + $HOME
  + $PWD
  + $SHELL
  + $USER
+ **自定义变量**
  + 变量=值
    + **等号两边不能有空格**
  + 撤销变量
    + `unset` 变量
  + `readonly`定义静态变量
  + 静态变量不能`unset`
  + 可以把一个变量提升为**全局环境变量**，可供其他shell使用

## SHELL环境变量

+ 基本语法
  + export 变量名=变量值 （将变量输出为环境变量）
  + source 配置文件
  + echo 变量名

## SHELL运算符

+ 基本语法
  + $((运算式)) 或者 $[运算式]
  + expr m + n,注意运算符之间需要加空格