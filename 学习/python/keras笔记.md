keras是一个可以在ten上运行的简单易学的高级python**深度学习库**。它可以让开发者只需将注意力放在深度学习的主要概念上，比如为神经网络创建层，与此同时它兼顾考虑了张量形状和数学细节等重要的部分。**ten可以说是keras的后端**。



## keras网络结构

+ 常见网络层
  + 常用层
    - dense层　全连接
    - activation层　　激活层
    - droupout　　　用于防止过拟合
    - flatten层　　　　把多维变成一维，常用于卷积层到全连接层的过渡
    - reshape层     用来将输入的shape转换成相应的shape
    - permute层　　RGB->GBR  维度重排

+ 模型概况查询

  + ```
    ＃　模型概况打印
    model.summary()
    
    # 返回代表模型的json字符串，仅包含网络结构，不包含权值
    from models import model_from_json
    
    json_model = model.to_json()
    model = model_from_json(json_model)
    
    # 权重获取
    model.get_layer()
    model.get_weights()
    ```

+ 模型的保存与加载

  ```
  model.save_weights(filepath)
  # 将模型权重保存到指定路径，文件类型是HDF5(后缀是.h5)
  
  model.load_weights(filepath, by_name=False)
  # 从h5文件中加载权重到当前模型中，默认情况下模型的结构保持不变
  
  # 模型和权值都保存到了本地
  model.save("model.h5")
  
  from keras.models import load_model
  
  load_model("model.h5")
  ```

+ 模型评估

  + predict
    + 返回预测值的numpy array
  + predict_classes
    + 返回预测结果
  + predict_proba
    + 返回预测的每个类别的概率

## Model式模型

+ 基本属性与训练流程
  + model.layers    添加层信息
  + model.compile   模型训练的BP模式设置
  + model.fit    模型训练的参数设置+训练
  + evaluate     模型评估
  + predict        模型预测
+ 常用Model属性
  + model.layers:组成模型的各个层
  + model.inputs：模型的输入张量列表
  + model.outputs：模型的输出张量列表

## 模型分类

+ 简单  **序列模型** sequential
+ 复杂   **函数式模型**



## 核心部分

+ **定义模型**。你可以创建一个序列模型并添加层。每一层可以包含一个或者多个卷积、池化、批量归一以及激活函数
+ **编译模型**
  + **compile方法**，接受三个参数
    
    + **optimizer**。它可以是现有优化器的字符串标识符，如rmsprop或adagrad,也可以是optimizer类的实例
    
    + **损失函数loss**,模型视图最小化的目标函数。categorical_crossentropy或mse,也可以是一个目标函数
    
    + **评测标准metrics**.对于任何分类问题，你都希望其设置为metrics=['accuracy']
    
      
    
    + ![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2019-11-26_16-58-51.png "常见配置")
+ **用训练数据拟合模型**
  
  + **fit方法**
    + **verbose参数**
      + 日志显示
      + **0** 不在标准输出流输出日志信息
      + **1** 输出进度条记录
      + **2** 每个epoch输出一行记录
      + **默认是1**
+ **预测**
  
  + **predict方法**

+ **评价**
  + **evaluate方法**
    + **verbose参数**
    + 日志显示
    + **0** 不在标准输出流输出日志信息
    + **1** 输出进度条记录
    + **只能取0或者1.默认是1**



## 深度学习过程

1. ### 载入数据

2. ### 预处理数据

3. ### 定义模型

4. ### 编译模型

5. ### 拟合模型

6. ### 评估模型

7. ### 预测

8. ### 保存模型

   1. ```python
      ## saving models
      
      model.save('model.h5')
      jsonmodel = model.to_json()
      model.save_weights('modelweights.h5')
      
      ## load weight of the saved model
      modelweight = model.load_weights("modelweight.h5")
      ```



## 改进keras模型的附加步骤

+ 当模型出现梯度消失或者梯度爆炸的原因，应该可以尝试以下操作；

+ ```python
from keras.callbacks import EarlyStopping
  
  early_stopping_monitor = EarlyStopping(patience=2)
  model.fit(x_train, y_train, batch_size=1000, epochs=10,
  	validation_data=(x_test, y_test),
  	callbacks=[early_stopping_monitor]
  )
  ```

## 迁移学习

+ 什么是迁移学习
  + 通常是指用训练好的模型解决第二个相关问题的过程
  + 在深度学习中，迁移学习是非常重要的技术，在该技术中，首先针对与现有问题类似的问题训练神经网络模型。然后，将训练中的模型的一层或者多层用于解决现有的问题的新模型。
+ 如何使用预训练模型
  + 分类器
    + 预训练模型直接用于分类新图像
  + 独立特征提取器
    + 预先训练的模型或模型的部分用于预处理图像并提取相关特征
  + 集成特征提取器
    + 预先训练的模型或模型的某些部分已集成到新模型中，但是在训练过程中冻结了预先训练的模型的各层。
  + 权重初始化
    + 将预训练模型或模型的某些部分集成到新模型中，与新模型一起预训练模型的各个层
+ 迁移学习模型
  + VGG(16或者19)
  + GOOGLENET(inceptionV3)
  + ResNet(ResNet50)



## Dropout层

+ ```python
  keras.layers.Dropout(rate, noise_shape=None, seed=None)
  ```
  + `防止过拟合`最简单的方法，假如随机噪声，输入层之后加入

## Tips

+ 模型需要知道它所期待的**输入尺寸**，顺序模型的**第一层**(且只有第一层，因为下面的层可以自动得推断尺寸)，需要接受关于其输入的尺寸信息。有下面几种做法：
  + 传递一个**input_shape**参数给第一层。它是一个表示尺寸的元祖(一个由整数或None组成的元祖)，在input_shape中不包含数据的batch大小
  + 某些2D层，例如Dense,支持通过参数input_dim指定输入尺寸，某些3D时许层支持input_dim和input_length参数
  + 如果需要为你的输入指定一个固定的batch大小，你可以传递一个batch_size参数给一个层。如果同时将batch_size=32和input_shape=(6, 8)传递给每一层，那么每一批的输入尺寸就为(32, 6, 8)。

+ model.summary()
  + ![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2019-11-28_13-58-58.png "模型总结")

+ 训练集、验证集、测试集的关系和区别

  + 训练集
    + 用来拟合模型，通过设置分类器的参数，训练模型

  + 验证集
    + 当通过训练集训练出多个模型后，为了能找出效果最佳的模型，使用各个模型对验证集数据进行预测，并记录模型的准确率。选出最佳的模型所对应的参数，即用来调整模型参数、

  + 测试集
    + 用来衡量该最优模型的性能和分类能力。可以把测试集当做从来不存在的数据集，当已经确定模型参数后，使用测试集进行模型性能评价

+ 总结
  + 对原始数据进行三个数据集的划分，也是为了防止模型过拟合。当使用了所有的原始数据去训练模型，得到的结果很可能是该模型最大程度地拟合原始数据，亦即该模型是为了拟合所有原始数据而存在。当新的样本出现，再使用该模型进行预测，效果可能还不如只使用一部分数据训练的模型。



## 可视化训练过程

```python
history = model.fit(X_train, y_train, batch_size=64, epochs=5, validation_split=0.2)

# 对accuracy进行可视化

plt.plot(history.history['accuracy'])
plt.plot(history.history['val_accuracy'])
plt.title('model accuracy')
plt.xlabel('epoch')
plt.ylabel('accuracy')
plt.legend(['train', 'validation'], loc='upper left')
plt.savefig('accuracy.png')
plt.show()

# 对loss进行可视化

plt.plot(history.history['loss'])
plt.plot(history.history['val_loss'])
plt.title('model loss')
plt.xlabel('epoch')
plt.ylabel('loss')
plt.legend(['train', 'validation'], loc='upper left')
plt.savefig("loss.png")
plt.show()
```

## 数据处理

### Keras.preprocessing库

+ text（只能处理英文，中文分词还是使用jieba）
  + 文字拆分
  + 建立索引
  + 序列补齐
  + 转换为矩阵
  + 使用标注类批量处理文本文件
+ sequence
+ image

