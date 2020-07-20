# Regression（回归）

回归所做的事情就是，生成一个函数，使得其根据给定的输入x，可以得到预期的输出y。

## Model（模型）

第一步就是选择Model。课程中介绍的第一个Model是Linear Model（线性模型）：

<a href="https://www.codecogs.com/eqnedit.php?latex=y=b&plus;{\sum}w_ix_i" target="_blank"><img src="https://latex.codecogs.com/png.latex?y=b&plus;{\sum}w_ix_i" title="y=b+{\sum}w_ix_i" /></a>

Model规定了最终生成的函数的格式，同时规定了待训练量

## Goodness of Function

接着，需要一个损失函数L用来评估函数的好坏。

其输入为函数本身，输出为函数的损失（how bad is it）<a href="https://www.codecogs.com/eqnedit.php?latex=L(f)" target="_blank"><img src="https://latex.codecogs.com/png.latex?L(f)" title="L(f)" /></a>

在Linear Model中，函数的本质是参数w和b，故有<a href="https://www.codecogs.com/eqnedit.php?latex=L(f)=L(w,b)" target="_blank"><img src="https://latex.codecogs.com/png.latex?L(f)=L(w,b)" title="L(f)=L(w,b)" /></a>

损失函数可以根据自己的需求来定，课程中使用平方误差来规定Linear Model的损失：

<a href="https://www.codecogs.com/eqnedit.php?latex=L(f)={\sum}_{i=1}^{n}(\hat{y}_i-(b&plus;w\cdot&space;x_i)))^2" target="_blank"><img src="https://latex.codecogs.com/png.latex?L(f)={\sum}_{i=1}^{n}(\hat{y}_i-(b&plus;w\cdot&space;x_i)))^2" title="L(f)={\sum}_{i=1}^{n}(\hat{y}_i-(b+w\cdot x_i)))^2" /></a>

显然，损失函数的值越小函数越好。

## Best Function

接着就是找到最佳的函数，使得损失函数最小。

对于Linear Model而言可以直接求解，但课程介绍了更为通用的Gradient Descent

### Gradient Descent（梯度下降）

梯度下降的本质是，针对函数<a href="https://www.codecogs.com/eqnedit.php?latex=L(w)" target="_blank"><img src="https://latex.codecogs.com/png.latex?L(w)" title="L(w)" /></a>，通过求导迭代逼近最低点。

具体操作方法如下：

1. 随机选择一个点<a href="https://www.codecogs.com/eqnedit.php?latex=w_0" target="_blank"><img src="https://latex.codecogs.com/png.latex?w_0" title="w_0" /></a>
2. 计算出函数<a href="https://www.codecogs.com/eqnedit.php?latex=L(w)" target="_blank"><img src="https://latex.codecogs.com/png.latex?L(w)" title="L(w)" /></a>在点<a href="https://www.codecogs.com/eqnedit.php?latex=w_0" target="_blank"><img src="https://latex.codecogs.com/png.latex?w_0" title="w_0" /></a>上的导数：<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{\mathrm{d}&space;L}{\mathrm{d}&space;w}|_{w=w_0}" target="_blank"><img src="https://latex.codecogs.com/png.latex?\frac{\mathrm{d}&space;L}{\mathrm{d}&space;w}|_{w=w_0}" title="\frac{\mathrm{d} L}{\mathrm{d} w}|_{w=w_0}" /></a>
3. <a href="https://www.codecogs.com/eqnedit.php?latex=w_1\leftarrow&space;w_0-\eta&space;\frac{\mathrm{d}&space;L}{\mathrm{d}&space;w}|_{w=w_0}" target="_blank"><img src="https://latex.codecogs.com/png.latex?w_1\leftarrow&space;w_0-\eta&space;\frac{\mathrm{d}&space;L}{\mathrm{d}&space;w}|_{w=w_0}" title="w_1\leftarrow w_0-\eta \frac{\mathrm{d} L}{\mathrm{d} w}|_{w=w_0}" /></a>
4. 重复迭代至收敛

这里我们定义<a href="https://www.codecogs.com/eqnedit.php?latex=\eta" target="_blank"><img src="https://latex.codecogs.com/png.latex?\eta" title="\eta" /></a>为Learning Rate（学习率），<a href="https://www.codecogs.com/eqnedit.php?latex=\bigtriangledown&space;L=\begin{bmatrix}&space;\frac{\mathrm{d}&space;L}{\mathrm{d}&space;w}&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/png.latex?\bigtriangledown&space;L=\begin{bmatrix}&space;\frac{\mathrm{d}&space;L}{\mathrm{d}&space;w}&space;\end{bmatrix}" title="\bigtriangledown L=\begin{bmatrix} \frac{\mathrm{d} L}{\mathrm{d} w} \end{bmatrix}" /></a>称之为Gradient（梯度）。

> 注意，这里的w，w0，w1都是一个向量，而不是单一变量或常量

#### 梯度下降的问题

显然，其最终寻找到的是一个极小值而非最小值。

但在Linear Model中不用担心这个问题，因为其损失函数是convex的（凸函数），故其极值点就是最值点。

## Model Selection

我们可以通过多项式的方法给Linear Model加参数，但这个导致的问题就是Overfitting。

于是我们需要根据test data上的数据来选取模型（而不是train data），取test data计算出来的损失函数值最小的Model。

## What are the hidden factor？

如果出现像这样的图，则说明x值不是唯一决定因素，会存在另一个factor在影响着结果：

<img src="img/1.png" />

上面这个图显然可以看出会有多个种类。现在假设这个种类是一个离散变量，那么我们可以这么改写模型：

<a href="https://www.codecogs.com/eqnedit.php?latex=\\y=b_1&plus;w_1x(x_s=A)&space;\\y=b_2&plus;w_2x(x_s=B)&space;\\y=b_3&plus;w_3x(x_s=C)&space;\\..." target="_blank"><img src="https://latex.codecogs.com/png.latex?\\y=b_1&plus;w_1x(x_s=A)&space;\\y=b_2&plus;w_2x(x_s=B)&space;\\y=b_3&plus;w_3x(x_s=C)&space;\\..." title="\\y=b_1+w_1x(x_s=A) \\y=b_2+w_2x(x_s=B) \\y=b_3+w_3x(x_s=C) \\..." /></a>

或者用激活函数来将其改写成一条式子：

<a href="https://www.codecogs.com/eqnedit.php?latex=\\y=b_1\delta(x_s=A)&plus;w_1\delta(x_s=A)x&space;\\&plus;b_2\delta(x_s=B)&plus;w_2\delta(x_s=B)x&space;\\&plus;b_3\delta(x_s=C)&plus;w_3\delta(x_s=C)x&space;\\&plus;..." target="_blank"><img src="https://latex.codecogs.com/png.latex?\\y=b_1\delta(x_s=A)&plus;w_1\delta(x_s=A)x&space;\\&plus;b_2\delta(x_s=B)&plus;w_2\delta(x_s=B)x&space;\\&plus;b_3\delta(x_s=C)&plus;w_3\delta(x_s=C)x&space;\\&plus;..." title="\\y=b_1\delta(x_s=A)+w_1\delta(x_s=A)x \\+b_2\delta(x_s=B)+w_2\delta(x_s=B)x \\+b_3\delta(x_s=C)+w_3\delta(x_s=C)x \\+..." /></a>

其中激活函数为：

<a href="https://www.codecogs.com/eqnedit.php?latex=\delta(x)=\left\{\begin{matrix}&space;1,&space;x=true\\&space;0,&space;x=false&space;\end{matrix}\right." target="_blank"><img src="https://latex.codecogs.com/png.latex?\delta(x)=\left\{\begin{matrix}&space;1,&space;x=true\\&space;0,&space;x=false&space;\end{matrix}\right." title="\delta(x)=\left\{\begin{matrix} 1, x=true\\ 0, x=false \end{matrix}\right." /></a>

其仍为Linear Model，照常训练即可。

## Regularization（正则化）

有时候会在Linear Model上加很多特征（或再加上其多项式特征），使得最终Overfitting。但又因为参数太多没办法一个一个试然后取test data上Loss最小的Model，这个时候就可以用Regularization。

其核心思想是惩罚复杂函数，使Model在不牺牲过多准确性的前提下尽可能平滑和简单。

那么惩罚显然是加在Loss里面的：

<a href="https://www.codecogs.com/eqnedit.php?latex=L(f)={\sum}_{i=1}^{n}(\hat{y}_i-(b&plus;w\cdot&space;x_i)))^2&plus;\lambda&space;w^2" target="_blank"><img src="https://latex.codecogs.com/png.latex?L(f)={\sum}_{i=1}^{n}(\hat{y}_i-(b&plus;w\cdot&space;x_i)))^2&plus;\lambda&space;w^2" title="L(f)={\sum}_{i=1}^{n}(\hat{y}_i-(b&plus;w\cdot&space;x_i)))^2+\lambda w^2" /></a>

其中<a href="https://www.codecogs.com/eqnedit.php?latex=\lambda" target="_blank"><img src="https://latex.codecogs.com/png.latex?\lambda" title="\lambda" /></a>为正则化参数，其值越高表示惩罚力度越大，最终的Model就会越平滑。

于是调整不同的正则化参数再分别训练，取出test data上Loss最小的函数即可。