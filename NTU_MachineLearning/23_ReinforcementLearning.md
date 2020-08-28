# Reinforcement Learning

> 强化学习是一个很大的课题，这里只讲了一些入门的知识

强化学习的核心思想是让机器自己从环境中学习。其主要流程如下图所示：

<img src="img/23_01.png" />

其主要分如下几个部分：

+ Environment：学习场景对应的环境
+ Agent：强化学习的本体，需要从Environment中学习的AI
+ Observation：Environment中的状态，Agent的输入
+ Action：Agent通过输入Observation得到的输出，表示其对状态的反映
+ Reward：Action会反馈到Environment中，而Environment会根据其效果给出Reward
  + Reward用于Agent调整自己的策略/模型参数

有一点需要注意的是，**不一定每次Action都有Reward**。

以下围棋为例，AI每走一步都不会得到Reward（可以理解为Reward=0），直到棋局结束，胜利则得到1，失败则得到-1。

> 其他方法计算Reward也可（例如按终局子差算），但本质是一样的。

## Actor

这里只会讲到其中一种比较简单的强化学习方法：Actor（部分论文也将其成为Policy）

其将Agent视为一个Function，将上面的流程图解释为下面的样子：

<img src="img/23_02.png" />

遵循机器学习的步骤，其学习也分为三步：

+ 构建模型
+ 定义目标
+ 训练逼近目标

### 构建模型

由于Actor的模型就是一个Function，所以其完全可以使用之前讲过的神经网络

使用Deep Model的强化学习就是深度强化学习（DRL）

Actor针对输入的Observation，产生其做每个Action的概率

> 例如学习玩游戏的AI，输入当前游戏画面，输出其各个操作的概率（例如按左键概率0.7，按右键概率0.2，按开火概率0.1）

然后再根据概率分布使用一个随机数生成器来决定最后输出的Action

> 注意不要直接输出概率最大的Action，不然很难学到低概率的情况（以及会出现类似石头剪刀布一直出石头的情况）

### 定义目标

从最开始的强化学习流程定义中，可以很清晰的知道Reward越大越好

但由于同样的模型且同样的环境下Reward不一定完全相同，故需要最大化的应该是Reward的期望值。

我们定义一次episode（游戏场景中可以理解为一局游戏之类的）包括如下动作：

+ 获得初始的Observation（s_1）
+ 根据s_1获得Action（a_1）
+ 由于a_1得到Reward（r_1）
+ 获得新的Observation（s_2）
+ 根据s_2获得Action（a_2）
+ 由于a_2得到Reward（r_2）
+ 。。。
+ 由于a_T得到Reward（r_T），episode结束

据此我们可以定义一次episode包含的状态列表<a href="https://www.codecogs.com/eqnedit.php?latex=\tau" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\tau" title="\tau" /></a>为：<a href="https://www.codecogs.com/eqnedit.php?latex=\tau=\{s_1,a_1,r_1,s_2,a_2,r_2,...,s_T,a_T,r_T\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\tau=\{s_1,a_1,r_1,s_2,a_2,r_2,...,s_T,a_T,r_T\}" title="\tau=\{s_1,a_1,r_1,s_2,a_2,r_2,...,s_T,a_T,r_T\}" /></a>

于是就有总Reward：<a href="https://www.codecogs.com/eqnedit.php?latex=R(\tau)=\sum_{t=1}^{T}r_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?R(\tau)=\sum_{t=1}^{T}r_t" title="R(\tau)=\sum_{t=1}^{T}r_t" /></a>

我们假设在模型参数为<a href="https://www.codecogs.com/eqnedit.php?latex=\theta" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\theta" title="\theta" /></a>的情况下，状态列表<a href="https://www.codecogs.com/eqnedit.php?latex=\tau" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\tau" title="\tau" /></a>出现的概率为<a href="https://www.codecogs.com/eqnedit.php?latex=P(\tau|\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(\tau|\theta)" title="P(\tau|\theta)" /></a>，于是就有该模型的Reward期望为：

<a href="https://www.codecogs.com/eqnedit.php?latex=\bar{R}(\theta)=\sum_{\tau}R(\tau)P(\tau|\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\bar{R}(\theta)=\sum_{\tau}R(\tau)P(\tau|\theta)" title="\bar{R}(\theta)=\sum_{\tau}R(\tau)P(\tau|\theta)" /></a>

显然状态列表<a href="https://www.codecogs.com/eqnedit.php?latex=\tau" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\tau" title="\tau" /></a>有无穷多种，我们可以直接让机器运行N次episode（理解为玩N次游戏），得到N个<a href="https://www.codecogs.com/eqnedit.php?latex=\tau" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\tau" title="\tau" /></a>。于是我们就可以近似将每个<a href="https://www.codecogs.com/eqnedit.php?latex=\tau" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\tau" title="\tau" /></a>出现的几率视为<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{1}{N}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{1}{N}" title="\frac{1}{N}" /></a>，于是期望可以近似计算为：

<a href="https://www.codecogs.com/eqnedit.php?latex=\bar{R}(\theta){\approx}\frac{1}{N}\sum_{n=1}^{N}R({\tau}_n)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\bar{R}(\theta){\approx}\frac{1}{N}\sum_{n=1}^{N}R({\tau}_n)" title="\bar{R}(\theta){\approx}\frac{1}{N}\sum_{n=1}^{N}R({\tau}_n)" /></a>

我们的目标就是让上面这个东西最大化

### 训练

在之前提到的Regression中，我们定义一个损失函数L，并用Gradient Descent令其最小化

而现在我们定义一个目标函数，但目标并不是让其最小化，而是反过来的，让其最大化

于是我们迭代的时候不再是沿Gradient减下去，而是反过来地，让其增加上去。这就是Gradient Ascent

<img src="img/23_04.png" />

于是我们的目标是算出<a href="https://www.codecogs.com/eqnedit.php?latex=\triangledown\bar{R}(\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\triangledown\bar{R}(\theta)" title="\triangledown\bar{R}(\theta)" /></a>，并用其做Gradient Ascent

回到目标函数的公式：<a href="https://www.codecogs.com/eqnedit.php?latex=\bar{R}(\theta)=\sum_{\tau}R(\tau)P(\tau|\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\bar{R}(\theta)=\sum_{\tau}R(\tau)P(\tau|\theta)" title="\bar{R}(\theta)=\sum_{\tau}R(\tau)P(\tau|\theta)" /></a>，可以发现在计算梯度的时候<a href="https://www.codecogs.com/eqnedit.php?latex=R(\tau)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?R(\tau)" title="R(\tau)" /></a>是常数项，于是可以得到：

<a href="https://www.codecogs.com/eqnedit.php?latex=\triangledown\bar{R}(\theta)=\sum_{\tau}R(\tau){\triangledown}P(\tau|\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\triangledown\bar{R}(\theta)=\sum_{\tau}R(\tau){\triangledown}P(\tau|\theta)" title="\triangledown\bar{R}(\theta)=\sum_{\tau}R(\tau){\triangledown}P(\tau|\theta)" /></a>

为了用上之前提到的近似，让上面的式子乘上<a href="https://www.codecogs.com/eqnedit.php?latex=P(\tau|\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(\tau|\theta)" title="P(\tau|\theta)" /></a>和除以<a href="https://www.codecogs.com/eqnedit.php?latex=P(\tau|\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(\tau|\theta)" title="P(\tau|\theta)" /></a>（相当于啥事都没做），可以得到：

<a href="https://www.codecogs.com/eqnedit.php?latex=\triangledown\bar{R}(\theta)=\sum_{\tau}R(\tau)P(\tau|\theta)\frac{{\triangledown}P(\tau|\theta)}{P(\tau|\theta)}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\triangledown\bar{R}(\theta)=\sum_{\tau}R(\tau)P(\tau|\theta)\frac{{\triangledown}P(\tau|\theta)}{P(\tau|\theta)}" title="\triangledown\bar{R}(\theta)=\sum_{\tau}R(\tau)P(\tau|\theta)\frac{{\triangledown}P(\tau|\theta)}{P(\tau|\theta)}" /></a>

进而得到：

<a href="https://www.codecogs.com/eqnedit.php?latex=\triangledown\bar{R}(\theta){\approx}\frac{1}{N}\sum_{n=1}^{N}R({\tau}_n)\frac{{\triangledown}P(\tau|\theta)}{P(\tau|\theta)}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\triangledown\bar{R}(\theta){\approx}\frac{1}{N}\sum_{n=1}^{N}R({\tau}_n)\frac{{\triangledown}P(\tau|\theta)}{P(\tau|\theta)}" title="\triangledown\bar{R}(\theta){\approx}\frac{1}{N}\sum_{n=1}^{N}R({\tau}_n)\frac{{\triangledown}P(\tau|\theta)}{P(\tau|\theta)}" /></a>

又由于（基础求导法则，怕忘记了所以记上）：

<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{1}{f(x)}\frac{df(x)}{dx}=\frac{d{\log}(f(x))}{dx}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{1}{f(x)}\frac{df(x)}{dx}=\frac{d{\log}(f(x))}{dx}" title="\frac{1}{f(x)}\frac{df(x)}{dx}=\frac{d{\log}(f(x))}{dx}" /></a>

于是有：

<a href="https://www.codecogs.com/eqnedit.php?latex=\triangledown\bar{R}(\theta){\approx}\frac{1}{N}\sum_{n=1}^{N}R({\tau}_n){\triangledown}{\log}P(\tau_n|\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\triangledown\bar{R}(\theta){\approx}\frac{1}{N}\sum_{n=1}^{N}R({\tau}_n){\triangledown}{\log}P(\tau_n|\theta)" title="\triangledown\bar{R}(\theta){\approx}\frac{1}{N}\sum_{n=1}^{N}R({\tau}_n){\triangledown}{\log}P(\tau_n|\theta)" /></a>

忽视常数项，问题转化为求<a href="https://www.codecogs.com/eqnedit.php?latex={\triangledown}{\log}P(\tau|\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?{\triangledown}{\log}P(\tau|\theta)" title="{\triangledown}{\log}P(\tau|\theta)" /></a>

由于：

<a href="https://www.codecogs.com/eqnedit.php?latex=P(\tau|\theta)=p(s_1)p(a_1|s_1,\theta)p(r_1,s_2|a_1,s_1)p(a_2|s_2,\theta)..." target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(\tau|\theta)=p(s_1)p(a_1|s_1,\theta)p(r_1,s_2|a_1,s_1)p(a_2|s_2,\theta)..." title="P(\tau|\theta)=p(s_1)p(a_1|s_1,\theta)p(r_1,s_2|a_1,s_1)p(a_2|s_2,\theta)..." /></a>

即为：

<a href="https://www.codecogs.com/eqnedit.php?latex=P(\tau|\theta)=p(s_1)\prod_{t=1}^{T}p(a_t|s_t,\theta)p(r_t,s_{t&plus;1}|a_t,s_t)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(\tau|\theta)=p(s_1)\prod_{t=1}^{T}p(a_t|s_t,\theta)p(r_t,s_{t&plus;1}|a_t,s_t)" title="P(\tau|\theta)=p(s_1)\prod_{t=1}^{T}p(a_t|s_t,\theta)p(r_t,s_{t+1}|a_t,s_t)" /></a>

两边求log，就有：

<a href="https://www.codecogs.com/eqnedit.php?latex={\log}P(\tau|\theta)={\log}p(s_1)&plus;\sum_{t=1}^{T}{\log}p(a_t|s_t,\theta)&plus;{\log}p(r_t,s_{t&plus;1}|a_t,s_t)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?{\log}P(\tau|\theta)={\log}p(s_1)&plus;\sum_{t=1}^{T}{\log}p(a_t|s_t,\theta)&plus;{\log}p(r_t,s_{t&plus;1}|a_t,s_t)" title="{\log}P(\tau|\theta)={\log}p(s_1)+\sum_{t=1}^{T}{\log}p(a_t|s_t,\theta)+{\log}p(r_t,s_{t+1}|a_t,s_t)" /></a>

上式只有<a href="https://www.codecogs.com/eqnedit.php?latex={\log}p(a_t|s_t,\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?{\log}p(a_t|s_t,\theta)" title="{\log}p(a_t|s_t,\theta)" /></a>这一项跟模型有关，故求偏导可得：

<a href="https://www.codecogs.com/eqnedit.php?latex=\triangledown{\log}P(\tau|\theta)=\sum_{t=1}^{T}\triangledown{\log}p(a_t|s_t,\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\triangledown{\log}P(\tau|\theta)=\sum_{t=1}^{T}\triangledown{\log}p(a_t|s_t,\theta)" title="\triangledown{\log}P(\tau|\theta)=\sum_{t=1}^{T}\triangledown{\log}p(a_t|s_t,\theta)" /></a>

这里面<a href="https://www.codecogs.com/eqnedit.php?latex={\log}p(a_t|s_t,\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?{\log}p(a_t|s_t,\theta)" title="{\log}p(a_t|s_t,\theta)" /></a>就是模型输入<a href="https://www.codecogs.com/eqnedit.php?latex=s_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?s_t" title="s_t" /></a>时的输出中，<a href="https://www.codecogs.com/eqnedit.php?latex=a_t" target="_blank"><img src="https://latex.codecogs.com/gif.latex?a_t" title="a_t" /></a>对应的概率。

整理一下可以得到最终式子：

<a href="https://www.codecogs.com/eqnedit.php?latex={\triangledown}\bar{R}(\theta)=\frac{1}{N}\sum_{n=1}^{N}\sum_{t=1}^{T}R({\tau}^n)\triangledown{\log}p(a_t^n|s_t^n,\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?{\triangledown}\bar{R}(\theta)=\frac{1}{N}\sum_{n=1}^{N}\sum_{t=1}^{T}R({\tau}^n)\triangledown{\log}p(a_t^n|s_t^n,\theta)" title="{\triangledown}\bar{R}(\theta)=\frac{1}{N}\sum_{n=1}^{N}\sum_{t=1}^{T}R({\tau}^n)\triangledown{\log}p(a_t^n|s_t^n,\theta)" /></a>

#### Add a Baseline

如果Reward只有正数的话，那么只要被随机到的局面其概率都会上升。这样对没有被随机到的局面就会有影响。

故一般会给总Reward一个偏置，使其均值尽可能为0：

<a href="https://www.codecogs.com/eqnedit.php?latex={\triangledown}\bar{R}(\theta)=\frac{1}{N}\sum_{n=1}^{N}\sum_{t=1}^{T}(R({\tau}^n)-b)\triangledown{\log}p(a_t^n|s_t^n,\theta)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?{\triangledown}\bar{R}(\theta)=\frac{1}{N}\sum_{n=1}^{N}\sum_{t=1}^{T}(R({\tau}^n)-b)\triangledown{\log}p(a_t^n|s_t^n,\theta)" title="{\triangledown}\bar{R}(\theta)=\frac{1}{N}\sum_{n=1}^{N}\sum_{t=1}^{T}(R({\tau}^n)-b)\triangledown{\log}p(a_t^n|s_t^n,\theta)" /></a>