# 第一讲 向量及其运算

## n维空间中的点

一个n维空间的点可以表示为<a href="https://www.codecogs.com/eqnedit.php?latex=(x_1,x_2,x_3,...,x_n)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?(x_1,x_2,x_3,...,x_n)" title="(x_1,x_2,x_3,...,x_n)" /></a>

## 向量

同样地，一个n维向量a表示为<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{pmatrix}&space;a_1\\&space;...\\&space;a_n&space;\end{pmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{pmatrix}&space;a_1\\&space;...\\&space;a_n&space;\end{pmatrix}" title="\begin{pmatrix} a_1\\ ...\\ a_n \end{pmatrix}" /></a>

## 向量空间

粗略地讲，假设全体向量属于一个集合V，这个集合V中的任意向量和数域F中的数字满足线性计算法则，那么就可以称V为定义在数域F上的**向量空间**

## 向量的线性组合

给定向量集<a href="https://www.codecogs.com/eqnedit.php?latex=\left\{\mathbf{x}_1,\mathbf{x}_2,...,\mathbf{x}_n\right\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\left\{\mathbf{x}_1,\mathbf{x}_2,...,\mathbf{x}_n\right\}" title="\left\{\mathbf{x}_1,\mathbf{x}_2,...,\mathbf{x}_n\right\}" /></a>，则对任意满足<a href="https://www.codecogs.com/eqnedit.php?latex=c_1\mathbf{x}_1&plus;c_2\mathbf{x}_2&plus;...&plus;c_n\mathbf{x}_n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?c_1\mathbf{x}_1&plus;c_2\mathbf{x}_2&plus;...&plus;c_n\mathbf{x}_n" title="c_1\mathbf{x}_1+c_2\mathbf{x}_2+...+c_n\mathbf{x}_n" /></a>的向量集构成前面的向量集的所有线性组合

## 向量的点积和长度

向量的点积（内积、数量积）定义为其各个维度的数值的积相加，也即：<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{v}\cdot\mathbf{w}=v_1w_1&plus;v_2w_2&plus;...&plus;v_nw_n" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{v}\cdot\mathbf{w}=v_1w_1&plus;v_2w_2&plus;...&plus;v_nw_n" title="\mathbf{v}\cdot\mathbf{w}=v_1w_1+v_2w_2+...+v_nw_n" /></a>

向量的长度定义为其与自身的点积的值开方，也即：<a href="https://www.codecogs.com/eqnedit.php?latex=\left\|\mathbf{v}\right\|=\sqrt{\mathbf{v}\cdot\mathbf{v}}=\sqrt{v_1^2&plus;v_2^2&plus;...&plus;v_n^2}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\left\|\mathbf{v}\right\|=\sqrt{\mathbf{v}\cdot\mathbf{v}}=\sqrt{v_1^2&plus;v_2^2&plus;...&plus;v_n^2}" title="\left\|\mathbf{v}\right\|=\sqrt{\mathbf{v}\cdot\mathbf{v}}=\sqrt{v_1^2+v_2^2+...+v_n^2}" /></a>

长度为1的向量称为**单位向量**，显然我们就可以得到将一个向量除以其长度就可以将其单位化

## 向量的夹角

一般而言，两向量夹角的余弦值为：<a href="https://www.codecogs.com/eqnedit.php?latex=\cos\theta=\frac{\mathbf{v}\cdot\mathbf{w}}{\left\|\mathbf{v}\right\|\left\|\mathbf{w}\right\|}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\cos\theta=\frac{\mathbf{v}\cdot\mathbf{w}}{\left\|\mathbf{v}\right\|\left\|\mathbf{w}\right\|}" title="\cos\theta=\frac{\mathbf{v}\cdot\mathbf{w}}{\left\|\mathbf{v}\right\|\left\|\mathbf{w}\right\|}" /></a>

由上可得，当<a href="https://www.codecogs.com/eqnedit.php?latex=\mathbf{v}\cdot\mathbf{w}=0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mathbf{v}\cdot\mathbf{w}=0" title="\mathbf{v}\cdot\mathbf{w}=0" /></a>时，两向量垂直

一般规定零向量与任何向量垂直

## 两个不等式

### Cauchy-Schwarz不等式

不等式为：<a href="https://www.codecogs.com/eqnedit.php?latex=|\mathbf{v}\cdot\mathbf{w}|\leqslant\left\|\mathbf{v}\right\|\left\|\mathbf{w}\right\|" target="_blank"><img src="https://latex.codecogs.com/gif.latex?|\mathbf{v}\cdot\mathbf{w}|\leqslant\left\|\mathbf{v}\right\|\left\|\mathbf{w}\right\|" title="|\mathbf{v}\cdot\mathbf{w}|\leqslant\left\|\mathbf{v}\right\|\left\|\mathbf{w}\right\|" /></a>

可以从两向量夹角余弦值求法得到<a href="https://www.codecogs.com/eqnedit.php?latex=|\cos\theta|=\frac{|\mathbf{v}\cdot\mathbf{w}|}{\left\|\mathbf{v}\right\|\left\|\mathbf{w}\right\|}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?|\cos\theta|=\frac{|\mathbf{v}\cdot\mathbf{w}|}{\left\|\mathbf{v}\right\|\left\|\mathbf{w}\right\|}" title="|\cos\theta|=\frac{|\mathbf{v}\cdot\mathbf{w}|}{\left\|\mathbf{v}\right\|\left\|\mathbf{w}\right\|}" /></a>，又由于<a href="https://www.codecogs.com/eqnedit.php?latex=|\cos\theta|\leqslant1" target="_blank"><img src="https://latex.codecogs.com/gif.latex?|\cos\theta|\leqslant1" title="|\cos\theta|\leqslant1" /></a>且等式分子分母均非负数，可得上述不等式

### 三角形不等式

不等式为：<a href="https://www.codecogs.com/eqnedit.php?latex=\left\|\mathbf{v}&plus;\mathbf{w}\right\|\leqslant\left\|\mathbf{v}\right\|&plus;\left\|\mathbf{w}\right\|" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\left\|\mathbf{v}&plus;\mathbf{w}\right\|\leqslant\left\|\mathbf{v}\right\|&plus;\left\|\mathbf{w}\right\|" title="\left\|\mathbf{v}+\mathbf{w}\right\|\leqslant\left\|\mathbf{v}\right\|+\left\|\mathbf{w}\right\|" /></a>

当且仅当向量w是向量v的非负倍数时等号成立

可以从三角形关系中得到