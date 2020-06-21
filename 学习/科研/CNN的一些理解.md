## 多个小卷积核如何替代大卷积核

> 大尺寸的卷积核可以带来更大的感受野，但也意味着更多的参数，[Rethinking the Inception Architecture for Computer Vision](https://yq.aliyun.com/go/articleRenderRedirect?spm=a2c4e.11153940.0.0.76783cb3pn9Ien&url=https%3A%2F%2Flink.zhihu.com%2F%3Ftarget%3Dhttp%253A%2F%2Farxiv.org%2Fabs%2F1512.00567)作者提出可以用2个连续的3x3卷积层组成的小网络代替单个5x5卷积层还可以保持感受野范围的同时减少参数量。

| 卷积核设置    | 参数个数     |
| ------------- | ------------ |
| 一个5x5       | 5x5+1=26     |
| 两个级联的3x3 | (3x3+1)x2=20 |

## 为什么卷积核一般是奇数*奇数

+ **更容易padding**
  + 在卷积时，我们有时候需要**卷积前后的尺寸不变**。这时候我们就需要用到padding。假设图像的大小，也就是被卷积对象的大小为nxn，卷积核大小为kxk，padding的幅度设为（k-1）/2时，卷积后的输出就为（n-k+2x（（k-1）/2））/1+1=n，即卷积输出为nxn，**保证了卷积前后尺寸不变**。但是如果k
    是偶数的话，（k-1）/2就不是整数了。
+ 更容易找到**卷积锚点**！
  + 在CNN中，进行卷积操作时一般会以卷积核模块的一个位置为基准进行**滑动**，这个基准通常就是**卷积核模块的中心**。若卷积核为奇数，卷积锚点很好找，自然就是卷积模块中心，但如果卷积核是偶数，这时候就没有办法确定了，让谁是锚点似乎都不怎么好。

## 1x1卷积核的作用

> 1x1卷积核，又称为网中网（Network in Network）
>
> [Network in Network](https://arxiv.org/abs/1312.4400)

+ ![](https://pic.downk.cc/item/5ed38bcac2a9a83be54fbd0b.jpg)
+ **升降维**
  + 当输入为6x6x32时，1x1卷积的形式是1x1x32，当只有一个1x1卷积核的时候，此时输出为6x6x1。此时便可以体会到1x1卷积的实质作用：**降维**。当1x1**卷积核的个数小于输入channels数量时**，即降维
+ **增加非线性**
  + 1*1卷积核，可以在**保持feature map尺度不变**的（即不损失分辨率）的前提下大幅增加非线性特性（**利用后接的非线性激活函数**），把网络做的很deep。一个filter对应卷积后得到一个feature map，不同的filter(不同的weight和bias)，卷积以后得到不同的feature map，提取不同的特征，得到对应的specialized neuron。
+ **跨通道信息交互**
  + 使用1x1卷积核，实现降维和升维的操作其实就是**channel间信息的线性组合变化**，3x3，64channels的卷积核后面添加一个1x1，28channels的卷积核，就变成了3x3，28channels的卷积核，**原来的64个channels就可以理解为跨通道线性组合变成了28channels**，这就是通道间的信息交互.只是在channel维度上做线性组合，W和H上是共享权值的sliding window