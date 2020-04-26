## 前言

+ **ten支持模型并行和数据并行**



## 基础

### 张量

+ **是对标量、向量和矩阵的泛化**
+ 可以被认为是n维数组
+ 0维张量叫做标量(scalar)
+ n维张量叫做向量(vector)
+ 属性
  + 名字(name)
  + 形状(shape)
  + 类型(type)

### 计算图

+ 由一系列ten操作排成的节点组成
+ ![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-01-14_16-12-03.png)

### 会话

+ 囊括了ten运行时的控制和状态
+ **拥有**并**管理**TensorFlow程序运行时的**所有资源**
+ 当**所有计算**完成之后需要**关闭会话**帮助系统回收资源
  + sess = tf.Session()
+ ![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-01-14_17-04-00.png)

### 常量与变量

+ 常量
  + 运行过程中不会改变的单元
  + constant_name = tf.constant(value)

+ 变量

  + 运行过程中会改变的单元
  + v = tf.Variable(value, name)
  + 个别变量初始化：
    + init_v = v.initializer()

  + 所有变量初始化:
    + init_v = tf.global_variables_initializer()

### tensorboard

+ 实线表示有数据流向经过
+ 虚线表示依赖关系，某个节点需要依赖其余的节点
+ tensorflow的可视化工具
+ 和tensor运行在不同进程中

### 占位符

+ tf.placeholder ,用来给变量占位置

+ tf.placeholder(dtype, shape=None, name=None)

+ ```python
  with tf.Session() as sess:
      result = sess.run(c, feed_dict={a:10, b:3.2})
      print(result)
  ```

  





## 如何工作

+ 程序通常被结构化为**构建阶段和执行阶段**
+ 构建阶段搭建具有**节点**(操作)和**边**(张量)的图
+ 执行阶段使用**会话来执行图中的操作**
+ ten具有一个默认的图来构建操作添加节点
+ 用**张量**表示数据，用**计算图**搭建神经网络，用**会话**执行计算图，优化线上的权重，得到模型。