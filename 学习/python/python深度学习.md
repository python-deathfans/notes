# 第一章 什么是深度学习

## 1.1 人工智能、机器学习、深度学习

+ ![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-02-27_04-43-47.png "三者关系")

+ 人工智慧
  + 努力将通常人类完成的智力任务自动化

+ 机器学习

  + ![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-02-27_04-46-31.png "发展过程")

  + 三要素
    + 输入数据点。假如任务是语音识别，那么数据点就是记录人们说话的声音文件
    + 预期输出的事例。对于语音识别任务，这些事例可能是人们根据声音文件整理生成的文本。
    + 衡量算法效果好坏的方法。主要是计算当前输出与真实输出的差距。

# 第二章 神经网络入门

## 2.1 神经网络剖析

+ 层

+ 输入数据和相应的目标
+ 损失函数
+ 优化器
  + ![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-02-27_05-17-40.png "四者关系")

注：

+ 为了在调节网络参数(比如训练的轮数)的同时，你可以将数据划分为训练集和验证集。但是由于数据点很少，验证集会非常小。因此，验证分数可能会有很大的波动。在这种情况下，最佳做法是使用K折交叉验证法。这种方法将可用数据划分为K个分区，实例化K个相同的模型，将每个模型在K-1个分区上训练，并在剩下的一个分区进行评估。模型的验证分数将等于K个验证分数的平均值。这种的代码也是很好实现的。
+ ![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-02-27_05-51-54.png "三折交叉验证")

+ ```python
  import numpy as np
  k = 4
  num_val_samples = len(train_data) // k
  num_epochs = 100
  all_scores = []
  for i in range(k):
  print('processing fold #', i)
  val_data = train_data[i * num_val_samples: (i + 1) * num_val_samples]
  val_targets = train_targets[i * num_val_samples: (i + 1) * num_val_samples]
  partial_train_data = np.concatenate(
  [train_data[:i * num_val_samples],
  train_data[(i + 1) * num_val_samples:]],
  axis=0)
  partial_train_targets = np.concatenate(
  [train_targets[:i * num_val_samples],
  train_targets[(i + 1) * num_val_samples:]],
  axis=0)
  model = build_model()
  model.fit(partial_train_data, partial_train_targets,
  epochs=num_epochs, batch_size=1, verbose=0)
  val_mse, val_mae = model.evaluate(val_data, val_targets, verbose=0)
  all_scores.append(val_mae)
  ```

小结：

+ 回归问题使用的损失函数和分类问题不同。回归常见的损失函数是MSE
+ 同样，回归问题使用的评估指标也与分类问题不同。常见的回归问题指标是平均绝对误差(MAE)
+ 如果输入数据的特征具有不同的取值范围，应该预先处理，对每个特征单独进行缩放
+ 如果可用训练数据较少，使用K折验证可用可靠的进行评估模型
+ 如果可用的训练数据很少，最好使用隐藏层较少(通常只有一到两个)的小型网络，以避免严重的过拟合。

# 第三章 机器学习基础

## 3.1 机器学习的四个分支

+ **监督学习**只是冰山一角——机器学习是非常宽泛的领域，其子领域的划分非常复杂。机器学习算法大致可分为四大类，我们将在接下来的四小节中依次介绍。

### 3.1.1 监督学习

+ `监督学习`是目前最常见的机器学习类型。给定一组样本（通常由人工标注），它可以学会将`输入数据映射到已知目标`［也叫标注（annotation）］。

+ 虽然监督学习主要包括分类和回归，但是还有很多奇特变体
  + 序列生成
  + 语法树预测
  + `目标检测`
  + `图像分割`

### 3.1.2 无监督学习

+ 无监督学习是指在**没有目标的情况下**寻找输入数据的有趣变换，其目的在于`数据可视化、数据压缩、数据去噪`或更好地理解数据中的相关性。**降维**和**聚类**是最常用的无监督学习的方法。

### 3.1.3 自监督学习

+ 自监督学习是**没有人工标注的标签**的监督学习，你可以将它看作没有人类参与的监督学习。标签仍然存在（因为总要有什么东西来监督学习过程），但它们是从输入数据中生成的，通常是使用启发式算法生成的。

### 3.1.4 强化学习

+ 在强化学习中，智能体（agent）接收有关其环境的信息，并学会选择使某种奖励最大化的行动。

## 3.2 数据预处理、特征工程和特征学习

### 3.2.1 神经网络的数据预处理

数据预处理的目的是使原始数据**更适于用神经网络处理**，包括`向量化`、`标准化`、`处理缺失值`和`特征提取`。

+ 向量化
  + 神经网络的所有输入和目标都必须是**浮点数张量**（在特定情况下可以是整数张量）。无论处理什么数据（声音、图像还是文本），都必须首先将其转换为**张量**，这一步叫作**数据向量化（data vectorization）**。例如，在前面两个文本分类的例子中，开始时文本都表示为整数列表（代表单词序列），然后我们用 one-hot 编码将其转换为 float32 格式的张量。在手写数字分类和预测房价的例子中，数据已经是向量形式，所以可以跳过这一步。

+ 标准化
  + 在手写数字分类的例子中，开始时图像数据被编码为 0~255 范围内的整数，表示灰度值。将这一数据输入网络之前，你需要将其转换为 float32 格式并除以 255，这样就得到 **0~1 范围**
  + 一般来说，输入数据具有以下特征：
    + 取值较小：大部分值都应该在0~1之间
    + 同质性：所有特征的取值都应该在大致相同的范围内
+ 处理缺失值
  + 一般来说，对于神经网络，将**缺失值设置为 0** 是安全的，只要 0 不是一个有意义的值。网络能够从数据中学到 0 意味着缺失数据，并且会忽略这个值。

## 3.3 过拟合与欠拟合

​		机器学习的根本问题是**优化和泛化之间的对立**。**优化**（optimization）是指调节模型以在训练数据上得到最佳性能（即机器学习中的学习），而**泛化**（generalization）是指训练好的模型在前所未见的数据上的性能好坏。机器学习的目的当然是得到良好的泛化，但你无法控制泛化，只能基于训练数据调节模型。

​		如果无法获取更多数据，次优解决方法是**调节模型允许存储的信息量**，或对模型允许存储的信息加以约束。如果一个网络只能记住几个模式，那么优化过程会迫使模型集中学习最重要的模式，这样更可能得到良好的泛化。这种降低过拟合的方法叫做**正则化**。

### 3.3.1 减小网络大小

​			防止过拟合的最简单的方法就是**减小模型大小**，即减少模型中**可学习参数的个数**（这由层数和每层的单元个数决定）。在深度学习中，模型中可学习参数的个数通常被称为模型的**容量**（capacity）。直观上来看，参数更多的模型拥有更大的记忆容量（memorization capacity），因此能够在训练样本和目标之间轻松地学会完美的字典式映射，这种映射没有任何泛化能力。始终牢记：**深度学习模型通常都很擅长拟合训练数据，但真正的挑战在于泛化，而不是拟合。**

​		要找到合适的模型大小，一般的工作流程是**开始时选择相对较少的层和参数**，然后**逐渐增加层的大小或增加新层**，直到这种增加对验证损失的影响变得很小。

### 3.3.2  添加权重正则化

一种常见的**降低过拟合的方法**就是强制让模型权重只能取较小的值，从而限制模型的复杂度，这使得权重值的分布更加规则（regular）。这种方法叫作**权重正则化**（weight regularization），其实现方法是向网络损失函数中添加与较大权重值相关的成本（cost）。

- [ ] L1 正则化（L1 regularization）：添加的成本与权重系数的绝对值［权重的 L1 范数（norm）］成正比。

- [ ]  L2 正则化（L2 regularization）：添加的成本与权重系数的平方（权重的 L2 范数）成正比。

### 3.3.3 添加droupout正则化

​		**dropout** 是神经网络最有效也**最常用的正则化方法**之一，它是由多伦多大学的 Geoffrey Hinton和他的学生开发的。对某一层使用 dropout，就是在训练过程中随机将该层的一些输出特征舍弃（设置为 0）。

## 3.4 开发到最后一层

+ ![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-03_06-23-32.png)

## 3.5 小结

+ 定义问题与要收集的数据。收集数据，有需要的话用标签来标注数据
+ 选择衡量问题成功的指标。需要在验证数据上监控那些指标
+ 确定评估方法，留出验证？K折验证？
+ 开发第一个比基准更好的模型，即一个具有统计功效的模型
+ 开发过拟合过程
+ 基于模型在验证数据上的性能来进行模型正则化与调节超参数 

# 第四章 深度学习用于计算机视觉

 ## 4.1 在小型数据集上从头训练卷积神经网络

### 4.1.1 基本策略-不做任何正则化

+ fit_generator

  + ```
    fit_generator(generator, steps_per_epoch=None, epochs=1, verbose=1, callbacks=None, validation_data=None, validation_steps=None, validation_freq=1, class_weight=None, max_queue_size=10, workers=1, use_multiprocessing=False, shuffle=True, initial_epoch=0)
    ```

  + **steps_per_epoch**   yield的次数

  + **validation_data**  验证集，可以是生成器，也可以是元组

  + **validation_steps** 如果是生成器，必须设置这个参数，等于验证集个数/batch

  + **workers**  是否使用多线程进行工作

+ image preprocessiong

  + ```
    keras.preprocessing.image.ImageDataGenerator(featurewise_center=False, samplewise_center=False, featurewise_std_normalization=False, samplewise_std_normalization=False, zca_whitening=False, zca_epsilon=1e-06, rotation_range=0, width_shift_range=0.0, height_shift_range=0.0, brightness_range=None, shear_range=0.0, zoom_range=0.0, channel_shift_range=0.0, fill_mode='nearest', cval=0.0, horizontal_flip=False, vertical_flip=False, rescale=None, preprocessing_function=None, data_format='channels_last', validation_split=0.0, interpolation_order=1, dtype='float32')
    ```

  + **rotation_range**: Int. Degree range for random rotations.
  + **width_shift_range**: Float, 1-D array-like or int
  + **height_shift_range**: Float, 1-D array-like or int
  + **brightness_range**: Tuple or list of two floats. Range for picking a brightness shift value from.
  + **shear_range**: Float. Shear Intensity (Shear angle in counter-clockwise direction in degrees)
  + **zoom_range**: Float or [lower, upper]. Range for random zoom. If a float, `[lower, upper] = [1-zoom_range, 1+zoom_range]`.
  + **horizontal_flip**: Boolean. Randomly flip inputs horizontally.
  + **vertical_flip**: Boolean. Randomly flip inputs vertically.
  + **rescale**: rescaling factor. Defaults to None. If None or 0, no rescaling is applied, otherwise we multiply the data by the value provided (after applying all other transformations).
  + **validation_split**: Float. Fraction of images reserved for validation (strictly between 0 and 1).

### 4.1.2 数据增强

### 4.1.3 用预训练网络做特征提取

+ 想要将深度学习应用于小型图像数据集，一种常见高效的方法是使用预训练网络。**预训练网络**是保存好的网络，之前已在大型数据集上训练好。如果数据集够大，完全可以将模型应用于一个完全不相干的问题上。这种学到的特征在不同问题之间的可移植性，是深度学习与许多早期浅层学习方法相比的重要优势，使得深度学习对小数据问题非常有效

+ 使用预训练网络有两种方法：

  + **特征提取**
  + **模型微调**

+ **特征提取**

  + 使用`之前网络`学到的表示来从新样本中提取有趣的特征。然后将这些特征输入到一个`新的分类器`，从头开始训练

  + ![](C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-04_05-25-09.png)

  + 模型中**更靠近底层**的层提取的是**局部的、高度通用**的特征图，而**更靠近顶层**的层提取的是更加**抽象**的概念，如果你的**新数据集与原始数据集相差很大**，**最好只使用模型的前几层来做特征提取**，不要使用整个卷积基。

  + ```python
    from keras.applications import VGG16
    
    conv_base = VGG16(
    		weights='imagenet',
    		include_top=False,
    		input_shape=(150, 150, 3)
    )
    ```

    + weights指定模型初始化的权重检查点
    + include_top指定模型最后是包含密集连接分类器
    + input_shape定义了传入网络的形状，默认是可以任意的输入

  + 接下来还可以分成两部

    + 在数据集上运行卷积基，输出保存成硬盘中的Numpy数组，然后用这个数据作为输入，**输入到独立的密集型连接分类器中**。这种方法速度快，计算代价低，因为对于每个输入图像只需运行一次卷积基，而卷积基是目前流程中计算代价最高的。但是这种方式**不允许使用数据增强**
    
    + ```python
      def extract_features(directory, sample_count):
      features = np.zeros(shape=(sample_count, 4, 4, 512))
      labels = np.zeros(shape=(sample_count))
      generator = datagen.flow_from_directory(
      directory,
      target_size=(150, 150),
      batch_size=batch_size,
      class_mode='binary')
      i = 0
      for inputs_batch, labels_batch in generator:
      features_batch = conv_base.predict(inputs_batch)
      features[i * batch_size : (i + 1) * batch_size] = features_batch
      labels[i * batch_size : (i + 1) * batch_size] = labels_batch
      i += 1
      if i * batch_size >= sample_count:
      break
      return features, labels
      ```
    
    + 在顶部添加Dense层来扩展已有模型，并在输入数据上端到端地运行整个模型。这样你可以使用数据增强，因为每个输入图像进入模型时都会经过卷积基。但是，这种情况计算代价比第一种高很多。但是必须在编译和训练模型之前，一定要‘冻结’卷积基。**冻结**一个或者多个层指的是在训练过程中保持权重不变。keras中冻结网络的方式是将其trainable属性设置为False.之后必须编译网络，使其生效。

### 4.1.4 对预训练网络进行微调

+ 另一种广泛使用的模型复用的方法是**模型微调**，与特征提取互为补充。对于用于特征提取的冻结的模型基，微调是指将其顶部的几层“解冻”,并将解冻的几层和新增加的部分(本例是全连接分类器)联合训练。之所以叫做**微调**，是因为它只是略微调整了所复用模型更加抽象的表示，以便让这些表示与手头的问题更加相关。

+ <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-05_05-34-41.png" style="zoom:80%;" />

+ ```python
  conv_base.trainable = True
  set_trainable = False
  for layer in conv_base.layers:
  if layer.name == 'block5_conv1':
  set_trainable = True
  if set_trainable:
  layer.trainable = True
  else:
  layer.trainable = False
  ```
  
  
  
+ 微调网络的步骤：
  
  + 在已经训练好的基网络上添加自定义网络
  + 冻结基网络
  + 训练所添加的部分
  + 解冻基网络的一些层
  + 联合训练解冻的这些层和添加的部分

### 4.1.5小结

+ 卷积神经网络是用于计算机视觉任务的最佳机器学习模型。即使在非常小的数据集上也可以从头开始训练一个卷积神经网络，而且得到的结果还是很不错

+ 在小型数据集上的主要问题是**过拟合**。在处理图像数据时，**数据增强**是一种降低过拟合的强大方法

+ 利用**特征提取**，可以很容易将现有的卷积神经网络复用于新的数据集。特别是对于小型图像数据集，这个方法非常的有价值

+ 作为特征提取的补充，你还可以使用**微调**，将现有模型之前学习到的一些数据表示应用于新问题。这种方法可以进一步提高模型性能

  

# 第五章 高级的深度学习最佳实践

- [ ] Keras函数时API
- [ ] 使用Keras回调函数
- [ ] 使用TensorBoard可视化工具
- [ ] 开发最先进模型的重要最佳实践



## 5.1 Keras的函数式API

+ 有些网络需要多输入，而有些网络在层与层之间有内部分支，这个使得网络看起来像是层构成的**图**，而不是线性叠加
+ 有些任务是多模态输入
  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-05_06-03-00.png" style="zoom:80%;" />

+ 有些任务是多输出
  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-05_06-04-13.png" style="zoom:80%;" />

+ 残差网络
  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-05_06-05-40.png" style="zoom:80%;" />

+ inception网络
  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-05_06-05-32.png" style="zoom:80%;" />

### 5.1.1 函数式API简介

+ ```python
  from keras import Input, layers
  input_tensor = Input(shape=(32,))
  dense = layers.Dense(32, activation='relu')
  output_tensor = dense(input_tensor)
  ```

### 5.1.2 多输入模型

+ <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-05_06-12-41.png" style="zoom:80%;" />

+ 使用函数式API实现上面的问答系统

  + ```python
    from keras.models import Model
    from keras import layers
    from keras import Input
    text_vocabulary_size = 10000
    question_vocabulary_size = 10000
    answer_vocabulary_size = 500
    text_input = Input(shape=(None,), dtype='int32', name='text')
    embedded_text = layers.Embedding(
    text_vocabulary_size, 64)(text_input)
    encoded_text = layers.LSTM(32)(embedded_text)
    question_input = Input(shape=(None,),
    dtype='int32',
    name='question')
    embedded_question = layers.Embedding(
    question_vocabulary_size, 32)(question_input)
    encoded_question = layers.LSTM(16)(embedded_question)
    concatenated = layers.concatenate([encoded_text, encoded_question],
    axis=-1)
    answer = layers.Dense(answer_vocabulary_size,
    activation='softmax')(concatenated)
    model = Model([text_input, question_input], answer)
    model.compile(optimizer='rmsprop',
    loss='categorical_crossentropy',
    metrics=['acc'])
    ```

## 5.2 使用Keras回调函数和TensorBoard来检查并监督深度学习模型

### 5.2.1 训练过程中将回调函数作用于模型

+ 训练模型时，很多事情一开始都无法预测。尤其是你不知道需要多少轮才能得到最佳验证损失。前面所有例子都采用这样一种策略：训练足够多的轮次，这时模型已经开始过拟合，根据这第一次运行来确定训练所需要的正确轮数，然后使用这个最佳轮数从头开始再启动一次新的训练。当然，这种方法很浪费。
+ 处理这个问题的更好方法是，当观测到验证损失不再改善时就停止训练。这可以使用 Keras回调函数来实现。
+ **回调函数（callback）**是在调用 fit 时传入模型的一个对象（即实现特定方法的类实例），它在训练过程中的不同时间点都会被模型调用。它可以访问关于模型状态与性能的所有可用数据，还可以采取行动：中断训练、保存模型、加载一组不同的权重或改变模型的状态。
+ 回调函数的一些**用法示例**如下所示。、
  +  模型检查点（**model checkpointing**）：在训练过程中的不同时间点保存模型的当前权重。
  + 提前终止（**early stopping**）：如果验证损失不再改善，则中断训练（当然，同时保存在训
    练过程中得到的最佳模型）。
  + 在训练过程中**动态调节**某些参数值：比如优化器的学习率。
  + 在训练过程中记录训练指标和验证指标，或将模型学到的表示**可视化**（这些表示也在不
    断更新）：你熟悉的 Keras 进度条就是一个回调函数！
+ keras.callbacks 模块包含许多内置的回调函数，下面列出了其中一些，但还有很多没
  有列出来。
  + keras.callbacks.ModelCheckpoint
    + 可以设置保存当前最佳的网络模型
  + keras.callbacks.EarlyStopping
    + 可以监控一些指标，当网络过拟合的时候就停止
    + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-05_06-38-22.png" style="zoom:60%;" />
  + keras.callbacks.ReduceLROnPlateau
    + 如果**验证损失**不再改善，你可以使用这个回调函数来**降低学习率**。在训练过程中如果出现了损失平台（loss plateau），那么增大或减小学习率都是跳出局部最小值的有效策略
    + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-05_06-40-52.png" style="zoom:67%;" />
  + keras.callbacks.CSVLogger
  + keras.callbacks.LearningRateScheduler

### 5.2.2 TensorBoard简介

+ TensorBoard 的主要用途是，在训练过程中帮助你以可视化的方法监控模型内部发生的一切。如果你监控了除模型最终损失之外的更多信息，那么可以更清楚地了解模型做了什么、没做什么，并且能够更快地取得进展。TensorBoard 具有下列巧妙的功能，都在浏览器中实现。
  + 在训练过程中以可视化的方式监控指标
  + 将模型架构可视化
  + 将激活和梯度的直方图可视化‘
  + 以三维的形式研究嵌入

+ <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-05_06-48-04.png" style="zoom:67%;" />

## 5.3 让模型性能发挥极致

### 5.3.1 高级架构模式

+ 标准化
  + 是一个大类方法，用于让机器学习模型看到的不同样本彼此之间更加相似，这有助于模型的学习和对于新数据的泛化。
  + 批标准化（batch normalization）是 Ioffe 和 Szegedy 在 2015 年提出的一种层的类型
    a （在Keras 中是 **BatchNormalization** ），即使在训练过程中均值和方差随时间发生变化，它也可以
    适应性地将数据标准化。**通常在卷积层或者dense层之后使用**。
+ 深度可分离卷积
  + 深度可分离卷积（depthwise separable convolution）层（ **SeparableConv2D** ）的作用：这个层对输入的每个通道分别执行空间卷积，然后通过逐点卷积（1×1 卷积）将输出通道混合，如图 7-16 所示。这相当于将**空间特征学习和通道特征学习**分开。
  + <img src="C:\Users\包志龙\Desktop\常用\file\mark down笔记\图片\Snipaste_2020-03-06_06-59-06.png" style="zoom:80%;" />
  + 如果只用有限的数据从头开始训练**小型模型**，这些优点就变得尤为重要

### 5.3.2 超参数优化

+ 构建深度学习模型时，你必须做出许多看似随意的决定：应该堆叠多少层？每层应该包含多少个单元或过滤器？激活应该使用 relu 还是其他函数？在某一层之后是否应该使用BatchNormalization ？应该使用多大的 dropout 比率？还有很多。这些在架构层面的参数叫作超参数（**hyperparameter**），以便将其与模型参数区分开来，**后者通过反向传播进行训练**。
+ 一般过程：
  + 选择一组超参数（自动选择）
  + 构建相应的模型
  + 将模型在训练数据上进行拟合，并衡量其在验证数据上的最终性能】
  + 选择要尝试的下一组超参数(自动选择)
  + 重复上述过程
  + 最后，衡量模型在测试数据上的性能

### 5.3.3 模型集成

+ 想要在一项任务上获得最佳结果，另一种强大的技术是**模型集成**（model ensembling）。集成是指将一系列不同模型的预测结果汇集到一起，从而得到更好的预测结果。观察机器学习竞赛，特别是 **Kaggle** 上的竞赛，你会发现优胜者都是将很多模型集成到一起，它必然可以打败任何单个模型，无论这个模型的表现多么好

+ **集成的模型**应该**尽可能好**，同时**尽可能不同**。这通常意味着使用非常不同的架构，甚至使用不同类型的机器学习方法。有一件事情基本上是不值得做的，就是**对相同的网络，使用不同的随机初始化多次独立训练**，然后集成。如果模型之间的唯一区别是随机初始化和训练数据的读取顺序，那么集成的多样性很小，与单一模型相比只会有微小的改进。

+ 发现有一种方法在实践中非常有效（但这一方法还没有推广到所有问题领域），就是将**基于树**的方法（比如随机森林或梯度提升树）和**深度神经网络**进行集成

  