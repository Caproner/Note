# Gradient Descent（梯度下降）

这里主要讲梯度下降的优化点和数学原理

## Tuning your learning rate

学习率不能太高也不能太低，太高会导致无法到达最低点，太低则会使其收敛速度变慢

### 自动调节学习率

学习率与每一步的步长线性相关，所以随着迭代次数增多，学习率可以越来越小。

有一个简单粗暴的方式让学习率随迭代次数增多而减少（t是迭代次数）：

<img src="img/1.png" />

### Adagrad

这是另外一种简单调整学习率的方法。其思想是给上面的已经修正过的学习率<a href="https://www.codecogs.com/eqnedit.php?latex={\mu}^t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?{\mu}^t" title="{\mu}^t" /></a>再除以目前为止所有偏导数的**root mean square**：

<img src="img/2.png" />

其中：

<img src="img/3.png" />

展开之后分子分母的<a href="https://www.codecogs.com/eqnedit.php?latex=\sqrt{\frac{1}{t&plus;1}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\sqrt{\frac{1}{t&plus;1}}" title="\sqrt{\frac{1}{t+1}}" /></a>可以消掉，于是变成：

<img src="img/4.png" />

## Stochastic Gradient Descent

这是一种更快的梯度下降。其每次迭代不会计算全部记录，而是随机取一条记录（或者按顺序取）

<img src="img/5.png" />

其可以在做到同样的计算量的情况下迭代更多次，并离目标更近：

<img src="img/6.png" />

## Feature Scaling

不同特征的数据范围可能会出现较大差异，使得梯度下降会走弯路。

故需要将特征进行标准化：

<img src="img/7.png" />

其中<a href="https://www.codecogs.com/eqnedit.php?latex=m_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?m_i" title="m_i" /></a>是第i个特征的平均值，<a href="https://www.codecogs.com/eqnedit.php?latex={\sigma}_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?{\sigma}_i" title="{\sigma}_i" /></a>是第i个特征的标准差

## Theory

这里讲的是梯度下降为什么可以让函数值往极值点收敛。

> 这里有个前置问题是，梯度下降真的能让函数值往极值点收敛吗？
>
> 答案是不一定，当学习率过高时梯度下降不会收敛。

梯度下降的本质是，每次从当前点的一定范围内找到**函数值最小的点**取代当前点：

<img src="img/8.png" />

### 回顾Taylor Series

高数学过，任何一个可无限微分的函数都可以进行泰勒展开：

<img src="img/9.png" />

只取前两项，就有：

<img src="img/10.png" />

当x离<a href="https://www.codecogs.com/eqnedit.php?latex=x_0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_0" title="x_0" /></a>越近，上述约等于越接近h(x)的值。

对于有两个参数的函数，同样可以类推：

<img src="img/11.png" />

回到问题，问题中假设函数只有两个参数，则我们需要求函数<a href="https://www.codecogs.com/eqnedit.php?latex=L(\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?L(\theta)" title="L(\theta)" /></a>在点<a href="https://www.codecogs.com/eqnedit.php?latex=(a,b)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(a,b)" title="(a,b)" /></a>的一定范围内的最小值。

通过Taylor Series可以近似得到：

<img src="img/12.png" />

将一些常数用字母代替：

<img src="img/13.png" />

可以得到：

<img src="img/14.png" />

设一定范围为一个半径为d的圆，那么<a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a>必须在满足<a href="https://www.codecogs.com/eqnedit.php?latex=(\theta_1-a)^2&plus;(\theta_2-b)^2{\leq}d^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(\theta_1-a)^2&plus;(\theta_2-b)^2{\leq}d^2" title="(\theta_1-a)^2+(\theta_2-b)^2{\leq}d^2" /></a>的情况下，使<a href="https://www.codecogs.com/eqnedit.php?latex=u(\theta_1-a)&plus;v(\theta_2-b)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u(\theta_1-a)&plus;v(\theta_2-b)" title="u(\theta_1-a)+v(\theta_2-b)" /></a>最小。

而<a href="https://www.codecogs.com/eqnedit.php?latex=u(\theta_1-a)&plus;v(\theta_2-b)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u(\theta_1-a)&plus;v(\theta_2-b)" title="u(\theta_1-a)+v(\theta_2-b)" /></a>可以看做是向量<a href="https://www.codecogs.com/eqnedit.php?latex=<u,&space;v>" target="_blank"><img src="https://latex.codecogs.com/gif.latex?<u,&space;v>" title="<u, v>" /></a>和向量<a href="https://www.codecogs.com/eqnedit.php?latex=<(\theta_1-a),(\theta_2-b)>" target="_blank"><img src="https://latex.codecogs.com/gif.latex?<(\theta_1-a),(\theta_2-b)>" title="<(\theta_1-a),(\theta_2-b)>" /></a>的点积，而<a href="https://www.codecogs.com/eqnedit.php?latex=(\theta_1-a)^2&plus;(\theta_2-b)^2{\leq}d^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(\theta_1-a)^2&plus;(\theta_2-b)^2{\leq}d^2" title="(\theta_1-a)^2+(\theta_2-b)^2{\leq}d^2" />则可以看做是向量<a href="https://www.codecogs.com/eqnedit.php?latex=<(\theta_1-a),(\theta_2-b)>" target="_blank"><img src="https://latex.codecogs.com/gif.latex?<(\theta_1-a),(\theta_2-b)>" title="<(\theta_1-a),(\theta_2-b)>" /></a>的长度不能超过d。

于是显然地，当向量<a href="https://www.codecogs.com/eqnedit.php?latex=<(\theta_1-a),(\theta_2-b)>" target="_blank"><img src="https://latex.codecogs.com/gif.latex?<(\theta_1-a),(\theta_2-b)>" title="<(\theta_1-a),(\theta_2-b)>" /></a>和<img src="https://latex.codecogs.com/gif.latex?<u,&space;v>" title="<u, v>" />方向相反即可。于是可以得到：

<img src="img/15.png" />

其中学习率用于控制长度不要超过d（也就是范围不要太宽，不然泰勒展开的准确度会下降）。

展开得到：

<img src="img/16.png" />

这就是梯度下降的式子了。