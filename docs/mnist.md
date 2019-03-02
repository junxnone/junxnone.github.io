MNIST是一个入门级的计算机视觉数据集，它包含各种手写数字图片.

# Reference
- [ ] [mnist beginners - tensorfly](http://tensorfly.cn/tfdoc/tutorials/mnist_beginners.html)
- [ ] [Visualizing MNIST](http://colah.github.io/posts/2014-10-Visualizing-MNIST/)
- [ ] [THE MNIST DATABASE of handwritten digits](http://yann.lecun.com/exdb/mnist/)
- [ ] [Notebook: Get Started with TensorFlow - mnist](https://colab.research.google.com/github/tensorflow/models/blob/master/samples/core/get_started/_index.ipynb#scrollTo=3wF5wszaj97Y)
- [ ] [Fashion-MNIST](https://github.com/zalandoresearch/fashion-mnist)

# [Source Code](https://github.com/junxnone/tech-io/issues/8#issuecomment-414728327)
## Step-1 Load Data
```
(x_train, y_train), (x_test, y_test) = mnist.load_data()
```
Download the [mnist dataset](https://storage.googleapis.com/tensorflow/tf-keras-datasets/mnist.npz) and load the train data & test data


**load_data():**
[tensorflow/python/keras/datasets/mnist.py](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/python/keras/datasets/mnist.py#L28)

---
## Step-2 Build model 
Build the tf.keras model by stacking layers. Select an optimizer and loss function used for training:
```
model = tf.keras.models.Sequential([
  tf.keras.layers.Flatten(),
  tf.keras.layers.Dense(512, activation=tf.nn.relu),
  tf.keras.layers.Dropout(0.2),
  tf.keras.layers.Dense(10, activation=tf.nn.softmax)
])

model.compile(optimizer='adam',
              loss='sparse_categorical_crossentropy',
              metrics=['accuracy'])
```
### Layers
- Flatten
- Dense
  - relu
  - softmax
- Dropout

*N.B. relu & softmax 为[激活函数](https://keras.io/zh/activations/)*

#### [Flatten Layer](https://keras.io/zh/layers/core/#flatten)
Flatten层用来将输入“压平”，即把多维的输入一维化，常用在从卷积层到全连接层的过渡。Flatten不影响batch的大小。
#### [Dense Layer](https://keras.io/zh/layers/core/#dense)
Dense就是常用的全连接层，所实现的运算是output = activation(dot(input, kernel)+bias)。其中activation是逐元素计算的激活函数，kernel是本层的权值矩阵，bias为偏置向量，只有当use_bias=True才会添加。

#### [Dropout Layer](https://keras.io/zh/layers/core/#dropout)
为输入数据施加Dropout。Dropout将在训练过程中每次更新参数时按一定概率（rate）随机断开输入神经元，Dropout层用于防止过拟合。

---
## Step-3 [complie model](https://keras.io/zh/getting-started/sequential-model-guide/#_2)
compile 接收三个参数：

- 优化器 optimizer。它可以是现有优化器的字符串标识符，如 rmsprop 或 adagrad，也可以是 Optimizer 类的实例。
- 损失函数 loss，模型试图最小化的目标函数。它可以是现有损失函数的字符串标识符，如 categorical_crossentropy 或  mse，也可以是一个目标函数。
- 评估标准 metrics。对于任何分类问题，你都希望将其设置为 metrics = ['accuracy']。评估标准可以是现有的标准的字符串标识符，也可以是自定义的评估标准函数。

### [optimizer - adam](https://keras.io/zh/optimizers/#adam)
### [loss - sparse_categorical_crossentropy](https://keras.io/zh/losses/#sparse_categorical_crossentropy)
### [Metrics - accuracy](https://keras.io/zh/metrics/)


---
## Step-4 [Train and evaluate model](https://keras.io/zh/getting-started/sequential-model-guide/#_3)
```
model.fit(x_train, y_train, epochs=5)

model.evaluate(x_test, y_test)
```
- [fit()](https://keras.io/zh/models/sequential/#fit)
以固定数量的轮次（数据集上的迭代）训练模型。
- [evaluate()](https://keras.io/zh/models/sequential/#evaluate)
在测试模式，返回误差值和评估标准值。计算逐批次进行。
# Colab Performance
Test with this [mnist_cnn.py](https://github.com/keras-team/keras/blob/master/examples/mnist_cnn.py) with [mnist_cnn.ipynb](https://colab.research.google.com/drive/1cK44hfBUtfAMGNtR2xhlYJu5I4rfnr6w)
## CPU
```
Epoch 1/12
60000/60000 [==============================] - 176s 3ms/step - loss: 0.2684 - acc: 0.9177 - val_loss: 0.0554 - val_acc: 0.9832
```
## GPU
```
Epoch 1/12
60000/60000 [==============================] - 10s 174us/step - loss: 0.2744 - acc: 0.9141 - val_loss: 0.0543 - val_acc: 0.9823
```
