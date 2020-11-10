> + Article记录文章标题
> + Data记录目的 结论 背景
> + Comments比较随意，记录自己的感想
> + Why记录对于自己的启发，可以是 了解课题背景 用于实验设计 写作模仿

[TOC]



## 01 Lightweight Deep Learning Model For Facial Expression Recognition

+ `Article`
  + **Lightweight Deep Learning Model For Facial Expression Recognition**
+ `Data`
  + 背景
    + 复杂的深度学习模型可以达到很好的效果，但是对于`资源受限的设备`，计算成本太高
    + 深度学习模型通常需要很高的计算和存储资源，这些资源不太受用于移动和嵌入式系统
  + 做法
    + 基于`MobileNet V2`
    + 数据增强
    + 网络结构
      + ![](https://pic.downk.cc/item/5f699789160a154a67271aeb.png)
      + ![](https://pic.downk.cc/item/5f699a06160a154a67288d2f.png)
      + ![](https://pic.downk.cc/item/5f699b1c160a154a6729382e.png)
      + `Inception Block`
        + 不同尺寸的过滤器相连，构造一个初始块来提取二维和三维通道特征
        + 提取特征
        + 权值共享
        + 稀疏连接
      + `bottleneck Block`
        + 基于反向残差块，深度可分离卷积网络。反向残差块具有相当高的内存成本效益
        + 用于降低非线性卷积操作，大幅度降低计算成本
      + `Conv+Pooling`
      + `全连接层`
  + 结论
    + 网络参数比InceptionResnet Inception小
    + 准确率高于MobileNet V2 Inception 和InceptionResnet网络
    + 网络在降低复杂度的同时，可以很好的保持准确度
+ `Comments`
  + Inception块、深度可分离卷积、反向残差块、瓶颈层(bottleneck)
+ `Why`
  + 实验设计
    + 实验中可以使用Inception块和深度可分离卷积设计网络
  + 写作设计
    + 网络结构图
    + 模型结构图
    + 超参数表格
    + 数据增强表格
    + 模型损失曲线、准确率图
    + 实验比较
      + 参数量
      + 准确率

## 02 Lightweight Deep Convolutional Neural Networks for Facial Expression Recognition

+ `Article`
  + **Lightweight Deep Convolutional Neural Networks for Facial Expression Recognition**
+ `Data`
  + **难点**
    + 表情因个体有差异，还有一些表情难以区分
  + **做法**
    + **深度可分离卷积**、**全局最大池化层**
    + 文章`没有直接使用预训练的VGG16`，而是先在`只有人脸图像组成的数据集上面进行预先训练自己的网络`，以捕捉与面部表情相关的更详细的特征。然后保留这些初始参数，使其保持训练网络的高精度，然后`再训练`。
  + **数据集**
    + `Fer2013`
    + AffectNet
  + **网络结构**
    + Baseline
      + `VGG`
      + `10层VGG网络`
        + 8个卷积层+2个全连接层
        + 得到证明，10层VGG在Fer2013上面达到最先进的精度
    + CCP模块
      + C 卷积层
      + P 池化层
      + F 全连接层
    + ![](https://pic.downk.cc/item/5f69b2ec160a154a6734cc51.png)
    + 网络再训练
    + ![](https://pic.downk.cc/item/5f69b517160a154a67359f05.png)
    + S代表`轻量化模块`，文中采用的是`深度可分离卷积`
    + GMP 代表的是`全局最大池化层`
      + 可以避免由于特征映射的大尺寸和参数减少而导致的过拟合
      + `替代了全连接层，大大减少参数的数量`
+ `Why`
  + 实验启发
    + 轻量化策略
      + 设计一个`VGG-like网络`，在`自己制作的数据集(表情识别数据集)`上面进行训练，`提取出前面几层网络`，在目标数据集上面进行再训练
      + `预训练网络+轻量化模块+GMP+F`
      + `全局最大池化层`可以替代全连接层，进一步缩小参数量。
    + 使用深度可分离卷积和全局最大池化层与包含最有意义的预训练网络层进行结合达到效果最好、模型参数最少的网络。

## 03 Facial Expression Recognition Method Based on Improved VGG Convolutional Neural Network

> + 教育方面，采用面部表情识别来观察课堂上学生的面部状态，从而判断学生在课堂上面的集中程度以及教师讲授的课程的吸引力
> + 现代医学中，观察患者情绪，及时向医生报告，医生可以分析和评估病情，为患者指定详细的康复计划
> + 可以提高医学水平标准，降低医疗费用
> + 犯罪分析方面，大量警察组织需要对犯罪嫌疑人进行长时间询问。表情识别可以作为分析犯罪嫌疑人心理变化的辅助手段，从而解决案件

+ `Data`
  + 数据集
    + `CK+`
  + 网络结构
    + base
      + VGG-19
    + 模型结构图
      + ![](https://pic.downk.cc/item/5f6bee70160a154a6732049a.png)
    + `冻结16层网络`，训练两个全连接层和输出层的参数
    + 模型压缩
      + 减少全连接层的个数
      + 迁移学习
      + 使用小的卷积核进行特征提取
+ `Why`
  + 实验设计
    + `VGG-19`网络，轻量化改进
    + CK+数据集

## 04 Facial Expression Recognition using Convolutional Neural Networks: State of the Art

+ `Data`
  + 实验方法
    + 数据预处理
    + CNN网络结构
    + 网络训练 与预测
  + Deep CNN
    + ![Snipaste_2020-09-25_08-53-50.png](https://i.loli.net/2020/09/25/xePTKlHEC3IWRr2.png)
    + VGG 每个CCP块之后加一个`Dropout块`，准确率可以提升1%
+ `Why`
  + 实验设计
    + 十层网络，效果最佳
    + 预训练十层网络

## 05 人脸表情识别综述

+ 文章内容
  + 传统的表情特征提取
  + 传统表情分类方法
  + 基于深度学习的表情识别方法
  + 对各种算法的识别率与性能进行了分析与比较
  + 常用数据集以及数据集的优势与存在的问题
  + 分析了GAN用于数据增强的技术与方法
+ 大纲
  + 中文摘要
  + 标题
  + 作者
  + 学校
  + 英文摘要
  + 关键词
  + 引言
    + **人脸表情的历史**
    + **表情识别技术的应用**
    + **表情识别的步骤**
    + **行文结构**
  + 传统表情识别方法
    + 特征提取
    + 表情识别
  + 基于深度学习的表情识别方法
  + 数据集以及常用的数据增强方法
    + GAN网络
  + 表情识别存在的问题以及未来的发展
  + 结束语
  + 参考文献

## 06 轻量化卷积神经网络研究与应用

+ baseline
  + `AlexNet`

`AlexNet`

+ 网络结构图
  + ![](https://pic.downk.cc/item/5f7eb4e01cd1bbb86babebb5.png)

+ 主要操作
  + 数据增强
  + LRN
  + Relu
  + Dropout
+ 改进
  + ![](https://pic.downk.cc/item/5f7eb3791cd1bbb86bab9e98.png)
  + ![](https://pic.downk.cc/item/5f7eb5ad1cd1bbb86bac350c.png)
  + 使用1x1卷积核，减少参数量
  + 轻量化改进
    + ![](https://pic.downk.cc/item/5f7ef0be1cd1bbb86bbccedd.png)
    + 增加卷积层的采样的多样性，同时增加了网络宽度和深度
    + 分组卷积+点卷积。
      + 由于3x3卷积和5x5卷积分布在不同组，所以组内缺少沟通，需要通过点卷积进行整合特征。

