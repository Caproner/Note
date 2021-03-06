# 第二章 数字系统

本章主要讨论如下内容：

+ 数字系统的定义
+ 位置化数字系统
+ 非位置化数字系统

## 什么是数字系统

通俗的讲就是表示数字的符号形式规则。也就是定义一套符号规则来唯一的表达唯一的一个数字。我们常用的十进制就是一个数字系统。

数字系统主要分为位置化数字系统和非位置化数字系统。前者更加常用。

## 位置化数字系统

在位置化数字系统中，数字中符号所占据的位置决定了其表示的值。

位置系统表示一个数字的基本形式为：

<img src="img/2_1.png" />

其值为：

<img src="img/2_2.png" />

其中：

+ S是一套符号系统，每个符号表示一个数值。数值从1开始并且是差为1的等差。
+ b是底（或称为基数），其表示S中的符号个数。

这么讲比较难理解（有点抽象），其实只要结合下面的例子就好理解了。

### 十进制系统

十进制系统中，基数为十，符号集S包括0到9这十个符号。

这是我们最常用的数字系统，故我们一般会省略底数表示。

这个就不用多讲吧。。。

### 二进制/八进制/十六进制系统

其实就是把底数换成2或8或16而已。

如果采用这种表示方式的话，为了跟十进制表示方式区分开，故需要将底数标出来。

特别说明的是，在十六进制系统中，符号集S包括了数字0到9和字母A到F，字母A到F分别表示十进制的10到15。

### 进制间转换

一般而言，将A进制的数字转换为B进制的数字分为两部：

+ 将A进制的数字转换为十进制
+ 将十进制的数字转换为B进制

#### 将其他进制转换为十进制

这个时候只需要用上前面提到的求值公式即可：

<img src="img/2_2.png" />

记得先将符号转换为十进制数字，例如说在十六进制转十进制的时候就需要把字母A换成数字10。

#### 将十进制转换为其他进制

先是将十进制数的整数部分和小数部分分开，两个部分分别计算。

##### 整数部分

整数部分利用类似连续除法的方法计算：

1. 创建一个空的字符串，这个字符串就是转换后的结果。
2. 将原本的十进制数字除以其他进制的底数，得到余数和商。
3. 将余数按照其他进制的字符集转换为对应的字符，从头部push进去（例如说将`6`从头部push进`A5`就会变成`6A5`）。
4. 如果商为0，那么完成转换，字符串即为最终结果。否则用商替换掉原本的十进制数，并回到步骤2。

##### 小数部分

弄懂了整数部分的转换方法之后，小数部分也就是类似了：

1. 创建一个空的字符串，这个字符串就是转换后的结果。

2. 将原本的十进制数字**乘以**其他进制的底数，得到结果。

   + 注意这里的十进制数字永远都是小于1的小数。

3. 将结果的整数部分提取出来，留下小数部分。

   + 整数部分记为A，如果没有整数部分那么A=0。

   + 此时这个十进制只剩小数部分，于是又会变为小于1的小数。

4. 将A按照其他进制的字符集转换为对应的字符，从**尾部**push进去（例如说将`6`从尾部push进`A5`就会变成`A56`）。

5. 如果此时十进制数为0，那么完成转换，字符串即为最终结果。否则回到步骤2。

##### 整合

最后只需要将整数部分和小数部分拼起来即可，记得中间加小数点。

#### 成幂次关系的进制间转换

所谓的成幂次关系可以理解为，假设A进制和B进制满足A的m次方等于B，那么他们就满足幂次关系。

这个时候他们之间的转换就有了更加简单的方式：**一一对应**

以二进制和十六进制为例。注意这里一直都要以**四**为单位的原因是2的4次方等于16。

要将二进制转换为十六进制只需要将二进制数字每四个数位转换为一个十六进制数位即可，位置不变。

例如说二进制数字`101110101010111`转换为十六进制

首先先按从低到高每四个为一组切分，就会变成`101 1101 0101 0111`。

接着只需要一个一个转就行了：

+ `101->5`
+ `1101->13->D`
+ `0101->5`
+ `0111->7`

于是其十六进制结果便是`5D57`。

从十六进制转回二进制也是一一对应的，只需要将十六进制的数位一个个转换为二进制数字（注意不足四位要补零）再拼起来就行了。

#### 求数字的长度

一个简单的问题是，将某个十进制数字转换成二进制数字，它的长度会有多长。

对于这个问题，我们可以不需要将这个数字转换出来才知道它的长度，而是可以通过求对数的方式来求。

举个例子，十进制数字`21987`的二进制长度就等于其以2为底的对数向下取整再加一，也就是：

<img src="img/2_3.png" />

> 这里在原书中的求法是以2为底的对数向上取整。但这个方法在遇到2的幂的时候就会发生错误。
>
> 举个例子，8在以2为底的对数是3（因为2的3次幂是8），但8转换为二进制是1000，有四位，故其是错的。
>
> 故将其修正为我上面说的方法。

## 非位置化数字系统

非位置化数字系统也会有自己的符号集，但其位置跟数位的大小并无关系。

典型的非位置化数字系统为罗马数字系统。

