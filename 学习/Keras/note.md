# 基础

## 模型保存和加载

+ 保存/加载整个模型(结构+权重+优化器状态)
  + `model.save(filepath)`
  + 将Keras模型保存到单个HDF5文件中
    + 模型结构
    + 模型权重
    + 训练配置项(损失函数，优化器)
    + 优化器状态
  + `keras.models.load_model(filepath)`
    + 模型加载
+ 只保存/加载模型的结构
  + `model.to_json()`
  + keras.models.model_from_json()
+ 只保存/加载模型的权重
  + `model.save_weights()`
  + model.load_weights()

## 如何冻结网络层

> 「冻结」一个层意味着将其排除在训练之外，即其权重将永远不会更新

+ 将trainable参数传递给一个层的构造器，将其设置为不可训练
  + `frozen_layer=Dense(32, trainable=False)`
+ 可以在实例化之后将网络层的trainable属性设置为True或者False。为了使之生效，在修改完属性之后，需要在模型上调用`compile()`。

# Sequential

## 模型编译

```python
# 多分类问题
model.compile(optimizer='rmsprop',
              loss='categorical_crossentropy',
              metrics=['accuracy'])

# 二分类问题
model.compile(optimizer='rmsprop',
              loss='binary_crossentropy',
              metrics=['accuracy'])

# 均方误差回归问题
model.compile(optimizer='rmsprop',
              loss='mse')

# 自定义评估标准函数
import keras.backend as K

def mean_pred(y_true, y_pred):
    return K.mean(y_pred)

model.compile(optimizer='rmsprop',
              loss='binary_crossentropy',
              metrics=['accuracy', mean_pred])
```



# Model

## 全连接网络

```python
from keras.layers import Input, Dense
from keras.models import Model

# 这部分返回一个张量
inputs = Input(shape=(784,))

# 层的实例是可调用的，它以张量为参数，并且返回一个张量
x = Dense(64, activation='relu')(inputs)
x = Dense(64, activation='relu')(x)
predictions = Dense(10, activation='softmax')(x)

# 这部分创建了一个包含输入层和三个全连接层的模型
model = Model(inputs=inputs, outputs=predictions)
model.compile(optimizer='rmsprop',
              loss='categorical_crossentropy',
              metrics=['accuracy'])
model.fit(data, labels)  # 开始训练
```

