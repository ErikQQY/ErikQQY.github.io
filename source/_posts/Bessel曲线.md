---
tags: 数学
---
# Bessel函数
对贝塞尔方程
$$
x^2y''+xy'+(x^2-n^2)y=0
$$
进行求解，过程有一些复杂具体运算在此&downarrow; &downarrow;

[利用广义幂级数求解Bessel方程](https://github.com/ErikQQY/ErikQQY.github.io/blob/master/Sources/BesselEquation.pdf)

### 第一类贝塞尔函数

也称作**贝塞尔函数**
$$
J_n(x)=\displaystyle\sum_{k=0}^{\infty}\frac{(-1)^k}{\Gamma(n+k+1)\Gamma(k+1)}(\frac{x}{2})^{2k+n}
$$
### 第二类贝塞尔函数
也称作**诺依曼函数**
$$
Y_n(x)=\displaystyle\sum_{k=0}^{\infty}\frac{(-1)^k}{\Gamma(-n+k+1)\Gamma(k+1)}(\frac{x}{2})^{2k-n}
$$
## 具体Bessel函数的一些性质：

* 性质1
	当$x\rightarrow\infty$，$J_n(x), Y_n(x)$有渐近式
	$$
	J_n(x)=\frac{A_n}{\sqrt(x)}[\sin(x+\alpha_n)+\omicron(1)]\\
	Y_n(x)=\frac{B_n}{\sqrt(x)}[\cos(x+\beta_n)+\omicron(1)]
	$$
* 性质2
	Bessel函数系在 $0\leq t\leq1$ 上为以 $t$ 为权的正交系
	$$
	\int_0^1tJ_n(\beta_jt)J_n(\beta_kt)dt=0\qquad j\neq k\\
	\int_0^1tJ_n(\beta_jt)J_n(\beta_kt)dt=\tau>0\qquad j=k
	$$