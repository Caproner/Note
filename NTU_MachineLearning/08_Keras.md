# Keras

Keras相当于TensorFlow的上层接口。如果要快速搭建机器学习模型的话适合使用Keras。

+ 官网：https://keras.io/
+ 自己鼓捣的Hello World：https://www.kaggle.com/caproner/ml2020-mission02
+ 对应的Kaggle比赛：https://www.kaggle.com/c/ml2020spring-hw2

有一点需要提的就是fit这里：

```python
history = model.fit(data, label, epochs=50, batch_size=4096)
```

这里用到一种介于Gradient Descent和SGD的方法：Mini-Batch。

其核心思想是，将数据随机分为大小为`batch_size`的batch，然后跑`epochs`次的epoch，每次epoch都会将所有的batch挨个塞进去训练一遍。

当`batch_size`为1的时候这就是SGD，而当`batch_size`为数据集大小时就是最普通的Gradient Descent。

其既可以加速迭代过程，又可以避开SGD大噪音的问题

> 看了网上的文档说batch_size一般是50~256，仅供参考。

