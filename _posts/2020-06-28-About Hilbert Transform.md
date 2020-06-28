# 希尔伯特变换（Hilbert Transform）的物理意义

## Hilbert变换简介

希尔伯特变换是信号处理中的一种常用手段，数学定义如下：

![希尔伯特变换的定义.jpg](https://i.loli.net/2020/06/23/umIqPJjipNyd2O1.png)

与卷积的概念进行对比，可以发现，上面的Hilbert变换的表达式实际上就是将原始信号和一个信号做卷积的结果。这个用来卷积的信号就是 
$$h(t)=\dfrac{1}{\pi t}​$$
希尔伯特变换从本质上来看是做了一次特殊的卷积积分，其中这个卷积的冲击响应为1/πt。换句话说，Hilbert变换可以看成是将原始信号通过一个滤波器或者一个系统，这个滤波器或系统的**冲击响应**为h(t)。

![希尔伯特变换的本质建模.jpg](https://i.loli.net/2020/06/23/tFVhUYJvmoZcB8M.png)

对h(t)做傅里叶变换，可以得到：
$$H(jω)=−j\,{\rm sgn}(ω)=
\left\{
\begin{array}{cc} 
		-j & \omega \ge 0\\ 
		j  & \omega < 0 
\end{array}
\right.$$
sgn()是符号函数。从频谱上来看，这个滤波器将我们的原始信号的正频率部分乘以 $-j$ ，而负频率部分乘以了 $j$ 。根据之前工程数学课程上的结论，Multiple a complex number by $j$ is to leave the modulus unaltered but to increase the argument by $\pi/2$。换句话说，上述系统响应的实质是在保持幅度不变的条件下，将正频率部分的相位移动了 $-\pi/2$ ；将负频率成分移动了 $\pi/2$ 。
从上述Hilbert变换可以看出，希尔伯特变换的作用上是一个90移相器，它将信号中的正频率部分相移-90°，相当于顺时针转90°；将信号中的负频率部分相移90°，相当于逆时针转90°。希尔伯特变换不会改变实信号x(t)的振幅和能量，仅仅在相位上发生了改变分而已。

下面这个示意图很直观地表示了Hilbert变换，这里画出了对原始信号做1到4次Hilbert变换的频谱示意图：

![希尔伯特变换示意图.jpg](https://i.loli.net/2020/06/23/jKQg9k2G7qsrPbZ.png)


首先，可以看到，两次希尔伯特变换后，原信号相位翻转了180°，所以，Hilbert逆变换的公式显而易见，就是将正变换加一个符号即可。另外，还可以看到，Hilbert变换四次后就变回本身了。还有其它的性质，比如：

*   如果一个信号是两个信号的卷积，即 $y = conv(v,x)$ ，那么 $Hilbert(y) = conv(Hilbert(v),x) = conv(v,Hilbert(x))$

*   $x(t)$ 和 $Hilbert(x(t))$ 的能量以及平均功率相等，相关函数和功率谱相同。

## Hilbert变换物理意义

### 解析过程概念
对于一个实随机过程 $x(t)$，$\hat{x}(t) = Hilbert(x(t))$ 为它的希尔伯特变换，那么定义复随机过程：
$$\tilde{x}(t) = x(t) + j\hat{x}(t)$$
为x(t)的**解析过程**。

这个过程有一个最重要的特点，就是解析信号的功率谱只有正频段，强度为原来的四倍。或者说是只有正频段且幅度值为原来的两倍(幅度与功率之间还有一次平方转换关系)：
$$
S_{\tilde{X}}(\omega)= 
\left\{
\begin{array}{cc} 
		4S_X(\omega) & \omega \ge 0\\ 
		0  & \omega < 0 
\end{array}
\right.
$$

### 欧拉公式（Euler‘s formula）的启发
欧拉公式：$e^{j\theta}=cos(\theta)+jsin(\theta)$
这个公式说明，用复指数信号可以表示成一个实数信号和一个虚数信号的和的形式。

| Functions | Fouier Transform |
|:---:|:---:|
|$cos(\omega_0t)$| $\pi[\delta(\omega+\omega_0)+\delta(\omega -\omega_0)]$ |
|$sin(\omega_0t)$| $j\pi[\delta(\omega+\omega_0)-\delta(\omega -\omega_0)]$ |

可以看出，在正频率上和负频率上两者的相位上的先后顺序刚好相反，但是都是保持90°的差值。欧拉公式实际上是一种特殊的 Hilbert 变换。
复指数信号 $e^{j\theta}$，频谱就是一个脉冲，而且是 $2\pi\delta(\omega - \omega_0)$。只有正频率，且是两倍。虽然时域上是复数，但是在频域只有正分量。

### 希尔伯特变换的意义

首先，将实数信号变换成解析信号的结果就是，把一个一维的信号变成了二维复平面上的信号，复数的模和幅角代表了信号的幅度和相位，如图所示：

![希尔伯特变换物理意义图](https://imgconvert.csdnimg.cn/aHR0cDovL2ltZy5ibG9nLmNzZG4ubmV0LzIwMTgwMjI1MDEyOTIzMjkx?x-oss-process=image/format,png)

这样看来，似乎复数信号才是完整的，而实信号只是在复平面的实轴上的一个投影。我们知道，解析信号可以计算包络（瞬时振幅）和瞬时相位。在上图中可以看到，实际上我们计算的包络就是黑色的线围成的立体图形的边界在实部的投影，而计算这个边的投影也很简单，就是在复平面上的螺旋线中的每一个点的模值，也就是 $A(t) = \sqrt{x^2(t) + Hilbert(x(t))^2}$ ，而瞬时相位就是虚部（Hilbert变换后的）和实部（原始信号）在某一时间点的比值的 arctan ，瞬时频率就是它的导数。