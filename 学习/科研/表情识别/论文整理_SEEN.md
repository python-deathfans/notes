## 01 Expression Recognition Method Based on a Lightweight Convolutional Neural Network

轻型网络

+ `数据集`
  + Fer2013
  + FerPlus

+ `DenseNet`
  + G. Huang, Z. Liu, L. V . D. Maaten, and K. Q. Weinberger, ‘‘Densely
    connected convolutional networks,’’ in Proc. IEEE Conf. Comput. Vis.
    Pattern Recognit. (CVPR), Jul. 2017, pp. 2261–2269.
  + H. Ma and T. Celik, ‘‘FER-Net: Facial expression recognition using
    densely connected convolutional network,’’ Electron. Lett., vol. 55, no. 4,
    pp. 184–186, Feb. 2019.
+ `SqueezeNet`
  + SQUEEZENET: ALEXNET-LEVEL ACCURACY WITH 50X FEWER PARAMETERS AND <0.5MB MODEL SIZE
+ `MobileNet`
  + Searching for MobileNetV3
+ `ShuffleNet`
  + ShuffleNet V2: Practical Guidelines for Efficient CNN Architecture Design

### 步骤

+ 人脸检测
  + 识别图像中的人脸，并对其进行标记，以备后续处理
  + `V-J检测器`
    + 效率很高，但是不能解决遮挡和大的姿态变化
  + `HOG+SVM`
    + 本篇文章
+ 人脸对齐
  + 解决人脸不正面时可能导致识别结果不准确的情况
  + 主流方法
    + 在定位面上找到`基准面和标记`，然后进行旋转和变形
    + AAM
+ 情感识别
  + DenseNet

### DenseNet

+ 两个参数
  + 增长率k
  + 稠密块 n

## 02 Facial Expression Recognition with Deep Learning 

+ 数据集
  + Fer2013
  + CK+
  + JAFFE
+ `ResNet50`
+ `SENET50`
+ `VGG16`

## 03 Facial Expression Recognition Based on Optimized ResNet 

> 减少模型参数并保持较高的识别精度

+ 网络
  + `ResNet`
  + `SENet`
  + 残差网络中嵌入SENet模块
+ 数据集
  + Fer2013
  + CK+
+ 工作量
  + 减小卷积核的大小、去除池化层、增加丢失层和融合SE模块
  + 研究网络层深对于精度的影响

## 04 Lightweight Deep Learning Model For Facial Expression Recognition

> 虽然现有的复杂的深度学习模型可以达到很高的精度，但是对于`资源受限`的设备，如`物联网设备 、移动端设备`，计算成本太高。
>
> 虽然有一些工作试图通过`缩小模型`的大小来降低模型的复杂性，但是由于`简单模型无法学习复杂的特征`，因此模型的性能会受到很大的影响。因此，在尽可能保持DNN模型检测性能的同时，提出了一些减小DNN模型规模的方法

`MobileNetV1`采用了`深度可分离的卷积`，以减小模型的大小并加快模型的速度。

 `inverted residual structure architecture` called `MobileNetV2`

本文基于`MobileNetV2`

### 网络结构

![](https://pic.downk.cc/item/5f4f457a160a154a67e0a048.png)



+ `Inception Block`
  + 采用不同尺寸的卷积核大小，避免特征丢失
+ `bottlenecks`
  + build on inverted residual blocks
  + `减少非线性运算`
  + 深度可分离卷积
    + MobileNetV1
    + depthwise convolutions
    + pointwise convolutions
  + Inverted residual with the linear bottleneck method
    + MobileNetV2
+ `fully connected layer`

### 实验部分

HYPER-PARAMETERS FOR DA TA AUGMENTA TION

| hyperparameters | values  |
| --------------- | ------- |
| rescale         | 1./255  |
| shear_range     | 0.2     |
| fill_mode       | nearest |
| horizontal_flip | True    |
| vertical_flip   | True    |

HYPER-PARAMETERS FOR MODEL TRAINING

| hyperparameters  | values      |
| ---------------- | ----------- |
| batch_size       | 16          |
| input_size       | 224, 224, 3 |
| optimization     | Adam        |
| epochs           | 200         |
| steps_per_epoch  | 256         |
| validation_steps | 64          |

+ 数据集

  + CK+

+ 数据增强

  