## 回调函数

> 训练模型时，很多事情一开始都无法预测。尤其是你不知道需要多少轮才能得到最佳验证损失。前面所有例子都采用这样一种策略：训练足够多的轮次，这时模型已经开始过拟合，根据这第一次运行来确定训练所需要的正确轮数，然后使用这个最佳轮数从头开始再启动一次新的训练。当然，这种方法很浪费。

+ `回调函数（callback）`是在调用`fit`时传入模型的一个对象（即实现特定方法的类实例），它在训练过程中的不同时间点都会被模型调用。它可以访问关于模型状态与性能的所有可用数据，还可以采取行动：`中断训练`、`保存模型`、加载一组不同的权重或改变模型的状态。
+ `模型检查点`(model check pointing):在训练过程中的不同时间点保存模型的当前权重。
+ `提前终止`(early stopping):如果验证损失不再改善，则中断训练(当然，同时保存在训练过程中得到的最佳模型)
+ `在训练过程中动态调节某些参数值`：比如优化器的学习率
+ 在训练过程中记录训练指标和验证指标，或将模型学到的表示`可视化`（这些表示也在不断更新）：你熟悉的Keras进度条就是一个回调函数！

### ModelCheckpoint与EarlyStopping回调函数

如果监控的`目标指标在设定的轮数内不再改善`，可以用`EarlyStopping`回调函数来`中断训练`。比如，这个回调函数可以在刚开始过拟合的时候就中断训练，从而避免用更少的轮次重新训练模型。这个回调函数通常与`ModelCheckpoint`结合使用，后者可以在训练过程中持续`不断地保存模型`（你也可以选择只保存目前的最佳模型，即一轮结束后具有最佳性能的模型）。

```python
import keras

# 因为回调函数需要验证集的精度，所以需要传入验证集

callbacks_list = [
	keras.callbacks.EarlyStopping(
		monitor='acc',
		patience=1,		# 如果精度在多于一轮的时间(即两轮)内不再改善，中断训练
	),
	keras.callbacks.ModelCheckpoint(
		filepath='my_model.h5',
		monitor='val_loss',
		save_best_only=True,		# 如果val_loss没有改善，那么就不需要覆盖模型文件，这样就可以始终保存最佳模型
	)
]

model.fit(
	X, Y,
	epoch=10,
	batch_size=32,
	callbacks=callbacks_list,
	validation_data = (x_val, y_val)
)
```

### ReduceLROnPlateau回调函数

如果`验证损失`不再改善，你可以使用这个回调函数来降低学习率。在训练过程中如果出现了损失平台（loss plateau），那么增大或减小学习率都是跳出局部最小值的有效策略。下面这个示例使用了ReduceLROnPlateau回调函数。

```python
callbacks_list = [
	keras.callbacks.ReduceLROnPlateau(
		monitor='val_loss',
		factor=0.1,  	# 触发时学习率除以10
		patience=10,	# 如果验证损失在10轮没有改善，那么就触发这个回调函数
	)
]

model.fit(
	X, Y,
	epoch=10,
	batch_size=32,
	callbacks=callbacks_list,
	validation_data = (x_val, y_val)
)
```



## TensorBoard

```
callbacks_list = [
	keras.callbacks.Tensorboard(
		log_dir='my_log_dir',		# 日志文件将被写入的位置
		histogram_freq=1,		# 每一轮之后记录激活直方图
		embeddings_freq=1,		# 每一轮之后记录嵌入数据
	)
]

model.fit(
	X, Y,
	epoch=10,
	batch_size=32,
	callbacks=callbacks_list,
	validation_data = (x_val, y_val)
)
```

+ cmd tensorboard --logdir=my_log_dir
+ http://localhost:6006