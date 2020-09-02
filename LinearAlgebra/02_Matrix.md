# 第二讲 矩阵与线性方程组

## 矩阵与向量的乘积

矩阵与向量的乘积方程里，如果向量是未知量，矩阵和乘积都是常数，则可以视该方程本质上就是在求解线性方程组

## 可逆矩阵

线性方程组<a href="https://www.codecogs.com/eqnedit.php?latex=A\mathbf{x}=\mathbf{b}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A\mathbf{x}=\mathbf{b}" title="A\mathbf{x}=\mathbf{b}" /></a>对任意向量b都有唯一解x的情况下，矩阵A就是可逆的

其逆可以从x的解得到。

例如下面的方程组：

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{pmatrix}&space;1&space;&&space;0&space;&&space;0\\&space;-1&space;&&space;1&space;&&space;0\\&space;0&space;&&space;-1&space;&&space;1&space;\end{pmatrix}&space;\begin{pmatrix}&space;x_1\\&space;x_2\\&space;x_3&space;\end{pmatrix}&space;=&space;\begin{pmatrix}&space;b_1\\&space;b_2\\&space;b_3&space;\end{pmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{pmatrix}&space;1&space;&&space;0&space;&&space;0\\&space;-1&space;&&space;1&space;&&space;0\\&space;0&space;&&space;-1&space;&&space;1&space;\end{pmatrix}&space;\begin{pmatrix}&space;x_1\\&space;x_2\\&space;x_3&space;\end{pmatrix}&space;=&space;\begin{pmatrix}&space;b_1\\&space;b_2\\&space;b_3&space;\end{pmatrix}" title="\begin{pmatrix} 1 & 0 & 0\\ -1 & 1 & 0\\ 0 & -1 & 1 \end{pmatrix} \begin{pmatrix} x_1\\ x_2\\ x_3 \end{pmatrix} = \begin{pmatrix} b_1\\ b_2\\ b_3 \end{pmatrix}" /></a>

可以解得：

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{cases}&space;x_1=b_1&space;&&space;\\&space;x_2=b_1&plus;b_2&space;&&space;\\&space;x_3=b_1&plus;b_2&plus;b_3&space;&&space;\end{cases}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{cases}&space;x_1=b_1&space;&&space;\\&space;x_2=b_1&plus;b_2&space;&&space;\\&space;x_3=b_1&plus;b_2&plus;b_3&space;&&space;\end{cases}" title="\begin{cases} x_1=b_1 & \\ x_2=b_1+b_2 & \\ x_3=b_1+b_2+b_3 & \end{cases}" /></a>

故可得上述矩阵可逆，其逆矩阵为：

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{pmatrix}&space;1&space;&&space;0&space;&&space;0\\&space;1&space;&&space;1&space;&&space;0\\&space;1&space;&&space;1&space;&&space;1&space;\end{pmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{pmatrix}&space;1&space;&&space;0&space;&&space;0\\&space;1&space;&&space;1&space;&&space;0\\&space;1&space;&&space;1&space;&&space;1&space;\end{pmatrix}" title="\begin{pmatrix} 1 & 0 & 0\\ 1 & 1 & 0\\ 1 & 1 & 1 \end{pmatrix}" /></a>

当一个矩阵可逆的时候，组成这个矩阵的向量**线性无关**，此时<a href="https://www.codecogs.com/eqnedit.php?latex=A\mathbf{x}=\mathbf{0}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A\mathbf{x}=\mathbf{0}" title="A\mathbf{x}=\mathbf{0}" /></a>只有零解

否则<a href="https://www.codecogs.com/eqnedit.php?latex=A\mathbf{x}=\mathbf{0}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A\mathbf{x}=\mathbf{0}" title="A\mathbf{x}=\mathbf{0}" /></a>有非零解，则矩阵A的组成向量线性相关，此时矩阵A为奇异矩阵

