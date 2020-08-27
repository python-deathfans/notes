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

## 04 Expression Recognition Method Based on a Lightweight Convolutional Neural Network





