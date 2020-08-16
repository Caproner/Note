# SVM

> 打个标记，看了之后还是对SVM不理解。知道它是干什么用的，但不知道为什么这么干。
>
> 之后看统计学习方法再去系统学一遍原理。

SVM（Supported Vector Machine）常用于分类问题，目标是创建一个超平面用于最好地分割不同类的数据。

其适用于分类问题。

## Linear SVM

其相比Logistics Regression而言只是换了一个Loss Function而已：

<img src="img/20_01.png" />

其可以用Gradient descent，也可以直接求解。

## Kernal Trick

我们假设<a href="https://www.codecogs.com/eqnedit.php?latex=w=Xa" target="_blank"><img src="https://latex.codecogs.com/gif.latex?w=Xa" title="w=Xa" /></a>，那就可以将函数按如下方式改写：

<img src="img/20_02.png" />

注意到<a href="https://www.codecogs.com/eqnedit.php?latex=(x^n&space;\cdot&space;x)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(x^n&space;\cdot&space;x)" title="(x^n \cdot x)" /></a>被定义为<a href="https://www.codecogs.com/eqnedit.php?latex=K(x^n,x)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?K(x^n,x)" title="K(x^n,x)" /></a>，这个就是Kernel Function。

然后做Gradient Descent：

<img src="img/20_03.png" />

可以发现，如果定义成这种形式，我们并不需要关系x的具体构造，只需要定义Kernel Function就可以求SVM了。

常用的Kernel Function有如下几种：

+ <a href="https://www.codecogs.com/eqnedit.php?latex=K(x,z)=(x&space;\cdot&space;z)^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?K(x,z)=(x&space;\cdot&space;z)^2" title="K(x,z)=(x \cdot z)^2" /></a>
+ <a href="https://www.codecogs.com/eqnedit.php?latex=K(x,z)=exp(-\frac{1}{2}\left&space;\|&space;x-z&space;\right&space;\|_2)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?K(x,z)=exp(-\frac{1}{2}\left&space;\|&space;x-z&space;\right&space;\|_2)" title="K(x,z)=exp(-\frac{1}{2}\left \| x-z \right \|_2)" /></a>
+ <a href="https://www.codecogs.com/eqnedit.php?latex=K(x,z)=tanh(x&space;\cdot&space;z)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?K(x,z)=tanh(x&space;\cdot&space;z)" title="K(x,z)=tanh(x \cdot z)" /></a>

Kernel Function会影响到SVM的分割函数的结构，令其可以不Linear。

