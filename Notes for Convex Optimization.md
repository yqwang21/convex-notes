# 0 引言

优化：从一个可行解的集合中寻找出最优的元素，一般形式如下
$$
\begin{align}
	&\text{minimize}\ \ \ \ f_0(x) \\
	&\text{s.t.} \ \ \ \ \ \ \ \ \ \ \ \ \ \ f_i(x)\le b_i,i=1,2,...,m
\end{align}
$$

+ objective function: $ f_0:R^n\rightarrow R$
+ inequality constraint: $f_i:R^n\rightarrow R$
+ optimization variance: $x=[x_1,x_2,...,x_n]^T$
+ optimal: $x^*$. For any $z$ with $f_1(z)\le b_1,...,f_m(z)\le b_m$, we have $f_0(z)\ge f_0(x^*)$

凸优化：objective function and constraint functions are convex:
$$
f_i(\alpha x + \beta y) \le \alpha f_i(x) + \beta f_i(y)\ \ \ \ \ \alpha+\beta=1,\alpha,\beta\ge 0
$$

# 1 凸集

## 1.1 仿射集和凸集

### 1.1.1 直线和线段

​		假设$x_1\neq x_2 \in R^n$，$\theta\in R$，此时定义
$$
y=\theta x_1 + (1-\theta)x_2
$$
则$y$是一条穿过$x_1,x_2$的直线. 若对$\theta$进行一定的限制，即$\theta\in[0,1]$，此时$y$为由$x_1,x_2$确定的一条线段. 当然，为了方便理解，可以将$y$的形式转化为
$$
y=x_2+\theta(x_1-x_2)
$$
<img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20211211154255459.png" alt="image-20211211154255459" style="zoom:75%;" />

### 1.1.2 仿射集

​		Affine Set：假设存在集合$C$，若$\forall x_1,x_2\in C$，穿过$x_1,x_2$的直线也在集合$C$内，则称集合$C$为**仿射集**. （$\forall x_1,x_2 \in C,\theta \in \boldsymbol{R}$，使得$\theta x_1+(1-\theta)x_2 \in C$）.

​		Affine Combination：假设存在集合$C$(不一定是仿射集)，有$x_1,\dots,x_k \in C$，且$\theta_1+\cdots+\theta_k=1$，称$\theta_1 x_1+\cdots+\theta_k x_k$为$x_1,\dots,x_k$的**仿射组合**. 
$$
\text{集合}\ C\ \text{是仿射集}\Leftrightarrow \text{任意元素的仿射组合} \in C
$$
​		假设集合$C$是仿射集，有$x_0\in C$，定义如下集合
$$
V=c-x_0=\{x-x_0|x\in C\}
$$
则称集合$V$是与$C$相关的**子空间**(subspace). 集合$V$有相较于一般的仿射集有更一般的性质：
$$
\forall x_1,x_2 \in V\ \text{和}\ \alpha,\beta \in \boldsymbol{R},\text{有}\ \alpha x_1+\beta x_2 \in V
$$
​		**线性方程组的解集是仿射集. **证明略	

​		Affine Hull：集合$C$的全部仿射组合的集合称为集合$C$的**仿射包**.
$$
\bold{aff}C=\{\theta_1x_1+\cdots+\theta_k x_k|x_1,\dots,x_k\in C, \theta_1+\cdots+\theta_k=1\}
$$
​		集合$C$的仿射包是包含集合$C$的最小的仿射集.

### 1.1.3 凸集

​		Convex Set：假设存在集合$C$，若$\forall x_1,x_2\in C$，由$x_1,x_2$确定的线段都在集合$C$内，则称集合$C$是**凸集**. （$\forall x_1,x_2\in C$和$\theta \in [0,1]$，使得$\theta x_1+(1-\theta)x_2 \in C$）.

​		从定义可以看出，仿射集一定是凸集.

​		Convex Combination: $\theta_1x_1+\cdots+\theta_kx_k$, where $\theta_1+\cdots+\theta_k=1$ and $\theta_1,\dots,\theta_k\in[0,1]$.
$$
 \text{集合}\ C\ \text{是凸集}\Leftrightarrow \text{任意元素的凸组合} \in C
$$

​		Convex Hull：集合$C$的所有凸组合的集合称为**凸包**.
$$
\bold{conv}C=\{\theta_1x_1+\cdots+\theta_kx_k|x_i\in C,\theta_i\ge 0,i=1,\dots,k,\theta_1+\cdots+\theta_k=1\}
$$
​		同理，集合$C$的凸包是包含集合$C$的最小的凸集.

### 1.1.4 锥

​		集合$C$是锥(cone) $\Leftrightarrow \forall x\in C,\theta\ge0$，有$\theta x\in C$.

​		集合$C$是凸锥(convex cone) $\Leftrightarrow \forall x_1,x_2\in C,\theta_1,\theta_2 \ge 0$，有$\theta_1x_1+\theta_2x_2\in C$.

​		凸锥组合(conic combination)： $\theta_1x_1+\cdots+\theta_kx_k$, where $\theta_1,\dots,\theta_k \ge 0$.

​		凸锥包(conic hull)：$\{\theta_1x_1+\cdots+\theta_kx_k|x_i\in C,\theta_i\ge 0,i=1,\dots,k\}$.

## 1.2 一些重要的例子

+ 空集$\emptyset$，单个点$\{x_0\}$，整个$R^n$面都是$R^n$的仿射子集（显然也是凸集）；
+ 任意直线都是仿射的，如果该直线经过原点，那么它也是凸锥；
+ 任意线段都是凸集，如果它缩短至一点，那么它也是仿射的；
+ 一条射线，即有表达式$\{x_0+\theta v|\theta\ge 0\},v\neq 0$，是凸集；当$x_0=0$时，它时凸锥；
+ $R^n$空间的子空间都是仿射集、凸集、凸锥.

### 1.2.1 超平面与半空间

​		超平面 *hyperplane*：$\{x|a^T x=b\}$, where $a\in \bold{R}^n$,$a\neq0$, and $b\in \bold{R}$.

<img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20211212154344079.png" alt="image-20211212154344079" style="zoom:75%;" />

+ 从数学分析角度，超平面是线性方程的解集，故是仿射集；
+ 从几何的角度，向量$a$作为平面的法向量(*normal vector*)，$b$作为平面相较于原点的偏移量.

​		一个超平面将$\bold{R}^n$空间分成两个半空间 *halfspaces*：$\{x|a^Tx\le b\}$ where $a\neq 0$. 

<img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20211212154405592.png" alt="image-20211212154405592" style="zoom:75%;" />

+ 半空间是凸集，但不是仿射的；
+ $\{x|a^T x < b\}$ is called an *open halfspace*.

### 1.2.2 欧几里得球和椭球

​		球 A (*Euclidean*) *ball* in $\bold{R}^n$ 有如下形式
$$
B(x_c,r)=\{x\ |\ ||x-x_c||_2\le r\}=\{x\ |\ (x-x_c)^T(x-x_c)\le r^2\}
$$
另一种表达形式为
$$
B(x_c,r)=\{x_c+ru\ | \ ||u||_2\le 1\}
$$


​		椭球 *ellipsoid*  有如下形式
$$
\mathcal{E}=\{x\ | \ (x-x_c)^T P^{-1}(x-x_c)\le 1\}
$$
式中$P=P^T\succ 0$，$P$是对称的正定矩阵. $\mathcal{E}$的半轴长度由$\sqrt{\lambda_i}$表示，$\lambda_i$是矩阵$P$的特征值. 当$P=r^2 I$时，椭球变成球.
+ 欧几里得球和椭球都是凸集.

### 1.2.3 多面体

​		多面体 *polyhedron* 被定义为有限个线性等式和线性不等式的解集：
$$
\mathcal{P}=\{x\ |\ a_j^Tx\le b_j,j=1,\dots,m,\ c_j^Tx=d_j,j=1,\dots,p \}
$$
由此可见，多面体是有限个半空间和超平面的交集. 仿射集、射线、线段和半空间都是多面体. 同时多面体也是凸集. 

<img src="C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20211212161059081.png" alt="image-20211212161059081" style="zoom:75%;" />

​		**单纯形** *simplex* 作为一种重要的多面体，有如下定义：

假设有$k+1$个点$v_0,\dots,v_k\in \bold{R}^n$，$v_1-v_0,\dots,v_k-v_0$是线性无关的，则与上述点相关的单纯形为
$$
C=\bold{conv}\{v_0,\dots,v_k \}=\{\theta_0v_0+\cdots+\theta_kv_k\ |\ \theta\succeq0,\bold{1}^T\theta=1 \}
$$

### 1.2.4 半正定锥

​		对称矩阵的集合：$\bold{S}^n=\{X\in \bold{R}^{n\times n}\ |\ X=X^T \}$

​		对称半正定矩阵的集合：$\bold{S}_+^n=\{X\in \bold{S}^n\ |\ X\succeq0  \}$

​		对称正定矩阵的集合：$\bold{S}_{++}^n=\{X\in\bold{S}^n\ |\ X\succ 0 \}$
