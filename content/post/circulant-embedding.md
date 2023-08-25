---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "循环嵌入法和分数布朗运动模拟"
subtitle: ""
summary: "通过将 Toeplitz 型的协方差矩阵嵌入成循环矩阵, 利用快速 Fourier 变换得到分数布朗运动的模拟."
authors: []
tags: []
categories: ['XX']
date: 2023-08-24T11:20:55+08:00
lastmod: 2023-08-24T11:20:55+08:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

## 记号

记 {{< math >}}$I_n${{< /math >}} 为 $n$ 阶单位矩阵, $O$ 为零矩阵, 上标 $T$ 表示转置, $H$ 表示共轭转置, $\bar{z}$ 表示复数 $z$ 的共轭, $\mathrm{diag}\\{\cdots\\}$ 表示对角矩阵, $\delta_{kj}$ 为 Kronecker 符号.
若 $f: \mathbb{R}^N \longrightarrow \mathbb{R}$, 记 $(\mathbb{R}^M)^{\otimes^N}\cong \mathbb{R}^{\overbrace{M\times \cdots \times M}^{N\text{个}}}$ 为 $\mathbb{R}^N$ 上的 $M$ 阶张量空间, $\\mathbf{n}=(n_1, \cdots, n_N)^T$, 
{{< math >}}
$$
 \mathbf{n}_{k\pm} := (n_1, \cdots, n_k \pm 1, \cdots, n_N)^T
 =(n_1, \cdots, n_k, \cdots, n_N)^T \pm (0, \cdots, 0, \mathop{1}\limits_{\text{kth}},0 \cdots, 0)^T,
$$
{{< /math >}}
{{< math >}}$f_{k\pm}(\mathbf{n}) := f(\mathbf{n}_{k\pm}).${{< /math >}}
$\mathbb{R}^{N}$ 上的离散 Laplace 算子 $\Delta$ 可看作是 $(\mathbb{R}^M)^{\otimes^N}$ 上的一个卷积核 $\Delta$. 若 {{< math >}}$\mathbf{X}=(f(\mathbf{k}))_{\mathbf{k}\in \mathbb{R}^N,\; \#\mathbf{k}=M^N} \in (\mathbb{R}^M)^{\otimes^N}${{< /math >}}, 则 $\mathbf{X}$ 作用离散Laplace算子后的 $\mathbf{k}$ 分量为
$$
(\Delta \mathbf{X})(\mathbf{k}) = (\mathbf{X} \ast \Delta)(\mathbf{k}) = \sum_{i=1}^{N}\left(f_{i+}(\mathbf{k})+f_{i-}(\mathbf{k})\right) - 2N f(\mathbf{k}),
$$
其中 $\ast$ 是卷积运算.

## 循环矩阵的特征值分解

$n$ 阶循环矩阵
{{< math >}}
$$
A = 
\begin{bmatrix}
a_0 & a_1 & a_2 & \cdots & a_{n-2} & a_{n-1} \\
a_{n-1} & a_0 & a_1 & \cdots & a_{n-3} & a_{n-2} \\
\vdots & \vdots & \vdots & \cdots & \vdots & \vdots \\
a_2 & a_3 & a_4 & \cdots & a_0 & a_1 \\
a_1 & a_2 & a_3 & \cdots & a_{n-1} & a_0
\end{bmatrix}
$$
{{< /math >}}
可由基本循环矩阵
{{< math >}}
$$
J = {
\begin{bmatrix}
 & 1 & & &  \\
&  & 1 & & \\
& &  & \ddots \\
& & & &1 \\
1&
\end{bmatrix}
}_{n\times n}
$$
{{< /math >}}
表示为
$$
A = a_0 I_n + a_1 J + a_2 J^2 + \cdots + a_{n-1}J^{n-1}.
$$
这是因为
{{< math >}}
$$
J^k =
\begin{bmatrix}
O & I_{n-k} \\
I_{k} & O
\end{bmatrix}, \qquad k=0,1,2,\cdots, n-1.
$$
{{< /math >}}
令
$$
g(x) = a_0 + a_1 x + a_2 x^2 + \cdots + a_{n-1}x^{n-1}, 
$$
则 $A = g(J)$. $J$ 的特征多项式 $\Delta_J(\lambda) = |\lambda I_n-J| = \lambda^n -1$, 所以 $J$ 的特征值$\lambda_k = \omega_k= e^{i2\pi k/n}$, $k=0,1,2, \cdots, n-1$. $\omega_k$ 对应的特征向量 $\alpha_k = (x_1, x_2, \cdots, x_n)^T$ 满足
$$
  \omega_k (x_1, x_2, \cdots, x_n)^T = (x_2, x_3, \cdots, x_1)^T,
$$
即
$$
\frac{x_2}{x_1} = \frac{x_3}{x_2} = \cdots = \frac{x_n}{x_{n-1}} = \frac{x_1}{x_n} = \omega_k
$$
或者
$$
x_m = x_1 \omega_k^{m-1}, \qquad m=1, 2,\cdots, n, 
$$
取 $x_1 = 1$, 可得 $J$ 的特征值 $\omega_k$ 对应的特征向量 $\alpha_k = (1, \omega_k, \omega_k^2, \cdots, \omega_k^{n-1})^T$, $k=0,1,2,\cdots, n-1$.

因为 $A=g(J)$, 所以 $A$ 的特征值为 $g(\omega_k)$, 对应的特征向量为 $\alpha_k$, $k=0,1,2, \cdots, n-1$, 因此 $A$ 有特征值分解 $A = P\Lambda P^{-1}$, 其中 $P = (\alpha_0, \alpha_1, \cdots, \alpha_{n-1})$, $\Lambda=\mathrm{diag}\\{g(\omega_0), g(\omega_1), \cdots, g(\omega_{n-1})\\}$.

注意到, $P = F^H$, $F$ 是离散 Fourier 变换矩阵, 并且
{{< math >}}
$$
\alpha_k^H \alpha_j = \sum_{m=0}^{n-1}\bar{\omega}_k^{m} \omega_j^m = \sum_{m=0}^{n-1} e^{-i2\pi km/n}e^{i2\pi jm/n} = \sum_{m=0}^{n-1}e^{i2\pi (j-k)m/n}= n\delta_{jk},
$$
$$
\begin{aligned}
\begin{bmatrix}
g(\omega_0) \\
g(\omega_1) \\
\vdots  \\
g(\omega_{n-1})
\end{bmatrix}
= 
\begin{bmatrix}
a_0 + a_1 \omega_0 + \cdots + a_{n-1}\omega_0^{n-1} \\
a_0 + a_1\omega_1 + \cdots + a_{n-1}\omega_1^{n-1} \\
\vdots  \\
a_0 + a_1\omega_{n-1} + \cdots + a_{n-1}\omega_{n-1}^{n-1}
\end{bmatrix}
= P^{T}
\begin{bmatrix}
a_0 \\
a_1 \\
\vdots  \\
a_{n-1}
\end{bmatrix}
= F^H
\begin{bmatrix}
a_0 \\
a_1 \\
\vdots  \\
a_{n-1}
\end{bmatrix},  
\end{aligned}
{{< /math >}}
$$
所以 $PP^H=nI_n$, 进而 $A = F^H \Lambda F/n$.

## 循环嵌入法

设 $Y(x)$ 是均值为0的平稳 Gauss 过程, 则对于任意的两个点 $x$, $y$, 存在相关函数 $r(\cdot)$ 使得协方差 $\mathbb{E}[Y(x)Y(y)]=r(|x-y|)$, 现在生成随机向量 $y=(Y(x_0), \cdots, Y(x_m))^{T} \sim \mathcal{N}(0, R)$, 其中协方差矩阵 {{< math >}}$R=(R_{pq})_{(m+1)\times (m+1)}=(r(|x_p-x_q|))_{(m+1)\times (m+1)}${{< /math >}}.

设 {{< math >}}$\Omega = \{x_0, \cdots, x_m\}${{< /math >}} 是均匀的节点,
那么协方差矩阵 $R$ 是一个半正定的对称 Toeplitz 矩阵, 于是 $R$ 可由首行向量 $r=(r_0, r_1, \cdots, r_m)$ 唯一确定, 其中 $r_k = r(|x_0 - x_k|)$. 
实际上, $R$ 显然是对称的. 另外由于 $\Omega$ 是均匀的, 所以 $R_{p+1, q+1}=r(|x_{p+1}-x_{q+1}|)=r(|x_p-x_q|)=R_{pq}$, 即 $R$ 是 Toeplitz 矩阵. 最后, 对于任意的 $u\in \mathbb{R}^{m+1}$, 
$$
u^T R u = u^T \mathbb{E}[yy^T] u =  \mathbb{E}[u^Tyy^Tu] = \mathbb{E}[(y^Tu)^T (y^Tu)] = Var(y^Tu) \geqslant 0,
$$
这里用到了正态分布的线性性 $y^Tu \sim \mathcal{N}(0, Var(y^Tu))$, 所以 $R$ 是半正定的.

为了生成 $y$, 需要将协方差矩阵 $R$ 嵌入到一个对称Toeplitz矩阵中使其变成一个循环矩阵. 设 $S$ 是一个 $(2M)\times (2M)$ 的对称Toeplitz矩阵, 其首行向量 $s=(s_0, \cdots, s_{2M-1})$ 定义为
$$ 
s_k = r_k,\quad k=0,\cdots, m,
\qquad
	s_{2M-k}=r_k, \quad k=1,\cdots, m-1,
$$
如果 $M>m$, $s_{m+1}, \cdots, s_{2M-m}$ 可取任意适合的值(下面要求 $S$ 半正定以满足 Gauss 过程的协方差矩阵的要求), 那么由上述方法 $R$ 嵌入得到的 $S$ 是一个循环矩阵, 并且沿主对角线的任意一个 $(m+1)\times (m+1)$ 块都等于 $R$. 由于 $S$ 是一个循环矩阵, 那么存在特征分解 $S=(1/(2M))F\Sigma F^{H}$, 其中 $F=(\exp(2\pi ipq/(2M)))_{0\leqslant p,q \leqslant 2M-1}$ 是离散 Fourier 变换矩阵, $\Sigma$ 是对角线向量为 $\tilde{s}=Fs$ 的对角矩阵,  由此可见, $S$ 半正定当且仅当 $\tilde{s}$ 中的元素非负.

下面假定 $S$ 是一个半正定矩阵.
令 $\varepsilon = \varepsilon_1 + i\varepsilon_2$ 是一个复随机向量, 其中 $\varepsilon_1$, $\varepsilon_2$ 是实 $2M$ 维的服从均值为0的正态分布
的随机向量, 且 $\mathbb{E}[\varepsilon_k \varepsilon_{j}^T]=\delta_{kj}I_{2M}$, 则我们有如下结论, 向量 $e=F(\Sigma/(2M))^{1/2}\varepsilon$ 的实部与虚部独立并且均服从于 $\mathcal{N}(0, S)$, 于是 $e$ 的实部和虚部的任意连续 $(m+1)$ 长的子向量独立且服从于 $\mathcal{N}(0, R)$. 事实上, 记 
{{< math >}}
$$
\begin{aligned}
F&=(\exp{2\pi i pq/(2M)})_{pq} \\
&=(\cos{(2\pi pq/(2M))})_{pq}+i(\sin{(2\pi pq/(2M))})_{pq} \\ 
&=:A+iB,
\end{aligned}
$$
$$
	D:= (\Sigma/(2M))^{1/2},
$$
{{< /math >}}
则
{{< math >}}
$$
\begin{aligned}
S = (A+iB)D^2(A-iB) = AD^2A + BD^2B, 
\end{aligned}
$$
$$
e = FD\varepsilon = (A+iB)D(\varepsilon_1 + i\varepsilon_2) = (AD\varepsilon_1-BD\varepsilon_2) +i(AD\varepsilon_2 + BD\varepsilon_1).
$$
{{< /math >}}
即
$$
BD^2A = AD^2B,
$$
$e$的实部是
$$
Re := Re(e) = AD\varepsilon_1-BD\varepsilon_2,
$$
虚部是
$$
Im := Im(e) = AD\varepsilon_2 + BD\varepsilon_1.
$$
于是, 
{{< math >}}
$$
\begin{aligned}
\mathbb{E}[Re Re^T]
&= \mathbb{E}[(AD\varepsilon_1 - BD\varepsilon_2)(\varepsilon_1^TDA-\varepsilon_2^TDB)] \\
&= AD\mathbb{E}[\varepsilon_1\varepsilon_1^T]DA + BD\mathbb{E}[\varepsilon_2\varepsilon_2^T]DB-AD\mathbb{E}[\varepsilon_1\varepsilon_2^T]DB-BD\mathbb{E}[\varepsilon_2\varepsilon_1^T]DA \\
&= AD^2A + BD^2B = S.
\end{aligned}
$$
{{< /math >}}
同理,
{{< math >}} 
$$
\mathbb{E}[Im Im^T]=S.
$$
$$
\begin{aligned}
\mathbb{E}[Re Im^T]
&= \mathbb{E}[(AD\varepsilon_1 - BD\varepsilon_2)(\varepsilon_2^TDA+\varepsilon_1^TDB)] \\
&= AD\mathbb{E}[\varepsilon_1\varepsilon_2^T]DA- BD\mathbb{E}[\varepsilon_2\varepsilon_1^T]DB+AD\mathbb{E}[\varepsilon_1\varepsilon_1^T]DB-BD\mathbb{E}[\varepsilon_2\varepsilon_2^T]DA \\
&= AD^2B-BD^2A = O.
\end{aligned}
$$
{{< /math >}}

循环嵌入法生成$m+1$维随机向量 $y\sim \mathcal{N}(0, R)$的步骤如下:
1. 将协方差矩阵 $R$ 嵌入到一个半正定的对称 Toeplitz 矩阵中得到一个 $(2M)\times (2M)$ 的循环矩阵 $S$, 使得 $s_k = r_k$, $k=0,\cdots, m$, $s_{2M-k}=r_k$, $k=1,\cdots, m-1$, 其中 $r$ 和 $s$ 分别为 $R$ 和 $S$ 的首行向量.
2. 通过快速傅里叶变换计算 $\tilde{s} =Fs$, 组成向量 $(\tilde{s}/(2M))^{1/2}$.
3. 生成 $2M$ 维向量 $\varepsilon = \varepsilon_1 + i\varepsilon_2$, 其中实随机向量 $\varepsilon_1$ 和 $\varepsilon_2$ 独立且都服从于 $\mathcal{N}(0, I_{2M})$.
4. 计算 $\tilde{e}=(\tilde{e}_k)= \varepsilon_k(\tilde{s}_k/(2M))^{1/2}$.
5. 使用快速傅里叶变换计算 $e=F\tilde{e}$, 则其实部和虚部的任意连续 $m+1$ 长的子向量独立且服从于 $\mathcal{N}(0, R)$.
6. 回到3进行循环生成不同的 $y$.

##  协方差

因为
$$
\mathbf{Y} = \Delta \mathbf{B},\qquad \mathbf{B} \in (\mathbb{R}^M)^{\otimes^N},
$$
{{< math >}}
所以协方差
$$
	\begin{aligned}
	\mathbf{C} &=	\mathbb{E}[\mathbf{Y}(\mathbf{n})({Y}(\mathbf{n}+\mathbf{k}))_{\mathbf{k}}] \\
	&= \mathbb{E}[\mathbf{Y}(\mathbf{n})({B}(\mathbf{n}+\mathbf{k}))_{\mathbf{k}} \ast \Delta ] \\
	&= \mathbb{E}[(\mathbf{Y}(\mathbf{n}){B}(\mathbf{n}+\mathbf{k}))_{\mathbf{k}}] \ast \Delta \\ 
	&= \mathbb{E}[((\mathbf{B} \ast \Delta)(\mathbf{n}){B}(\mathbf{n}+\mathbf{k}))_{\mathbf{k}}] \ast \Delta \\ 
	&=\left(\mathbb{E}[(\mathbf{B} \ast \Delta)(\mathbf{n}){B}(\mathbf{n}+\mathbf{k})]\right)_{\mathbf{k}} \ast \Delta \\ 	&=\left(\mathbb{E}\left[\left(\sum_{i=1}^{N}\left(B_{i+}(\mathbf{n})+B_{i-}(\mathbf{n})\right) - 2N B(\mathbf{n})\right){B}(\mathbf{n}+\mathbf{k})\right]\right)_{\mathbf{k}} \ast \Delta .
%	&= \left(\mathbb{E}\left[B(\mathbf{n}+\mathbf{k})\sum_{i=1}^NB_{i+}(\mathbf{k}) \right] - 2N \mathbb{E}\left[B(\mathbf{n}+\mathbf{k})B(\mathbf{k})\right]\right. \\
%	&+ \left.\mathbb{E}\left[B(\mathbf{n}+\mathbf{k})\sum_{i=1}^NB_{i-}(\mathbf{k}) \right]\right)_{\mathbf{k}} \ast \Delta 
	\end{aligned}\tag{1}
$$
{{< /math >}}
而
{{< math >}}
$$
	\begin{aligned}
		\mathbb{E}\left[B(\mathbf{n}+\mathbf{k})\sum_{i=1}^{N}B_{i+}(\mathbf{n})\right]&= 
		\sum_{i=1}^N\mathbb{E}[B(\mathbf{n}+\mathbf{k})B_{i+}(\mathbf{n})] \\
		&= \sum_{i=1}^N \mathbb{E}[B(\mathbf{n}+\mathbf{k})B(\mathbf{n}_{i+})] \\
		&= \frac{\sigma^2}{2}\sum_{i=1}^N \left(||\mathbf{n}+\mathbf{k}||^{2H}+||\mathbf{n}_{i+}||^{2H}-||\mathbf{n}+\mathbf{k} - \mathbf{n}_{i+}||^{2H}\right) \\
		&= \frac{\sigma^2}{2}\sum_{i=1}^N \left(||\mathbf{n}+\mathbf{k}||^{2H}+||\mathbf{n}_{i+}||^{2H}-||\mathbf{k}_{i-}||^{2H}\right) 
	\end{aligned}\tag{2}
$$
$$
	\begin{aligned}
		\mathbb{E}\left[B(\mathbf{n}+\mathbf{k})\sum_{i=1}^{N}B_{i-}(\mathbf{n})\right]&= 
		\sum_{i=1}^N\mathbb{E}[B(\mathbf{n}+\mathbf{k})B_{i-}(\mathbf{n})] \\
		&= \sum_{i=1}^N \mathbb{E}[B(\mathbf{n}+\mathbf{k})B(\mathbf{n}_{i-})] \\
		&= \frac{\sigma^2}{2}\sum_{i=1}^N \left(||\mathbf{n}+\mathbf{k}||^{2H}+||\mathbf{n}_{i-}||^{2H}-||\mathbf{n}+\mathbf{k} - \mathbf{n}_{i-}||^{2H}\right) \\
		&= \frac{\sigma^2}{2}\sum_{i=1}^N \left(||\mathbf{n}+\mathbf{k}||^{2H}+||\mathbf{n}_{i-}||^{2H}-||\mathbf{k}_{i+}||^{2H}\right) 
	\end{aligned}\tag{3}
$$
$$\mathbb{E}\left[B(\mathbf{n}+\mathbf{k})B(\mathbf{n})\right]=\frac{\sigma^2}{2} 
  \left(||\mathbf{n}+\mathbf{k}||^{2H}+||\mathbf{n}||^{2H}-||\mathbf{k}||^{2H}\right) \tag{4}
$$
{{< /math >}}
将 (2), (3), (4) 代入 (1), 得
{{< math >}}
$$
 \begin{aligned}
\mathbf{C} &= \frac{\sigma^2}{2}\left( \sum_{i=1}^N \left(||\mathbf{n}+\mathbf{k}||^{2H}+||\mathbf{n}_{i+}||^{2H}-||\mathbf{k}_{i-}||^{2H}\right) \right. \\
&-2N\left(||\mathbf{n}+\mathbf{k}||^{2H}+||\mathbf{n}||^{2H}-||\mathbf{k}||^{2H}\right) \\
& +\left.\sum_{i=1}^N \left(||\mathbf{n}+\mathbf{k}||^{2H}+||\mathbf{n}_{i-}||^{2H}-||\mathbf{k}_{i+}||^{2H}\right)\right)_{\mathbf{k}}\ast \Delta \\
&= \frac{\sigma^2}{2}\left(\sum_{i=1}^N (||\mathbf{n}_{i+}||^{2H} + ||\mathbf{n}_{i-}||^{2H}) - 2N||\mathbf{n}||^{2H} \right)_{\mathbf{k}}\ast \Delta \\
& -\frac{\sigma^2}{2}\left(\sum_{i=1}^N (||\mathbf{k}_{i+}||^{2H} + ||\mathbf{k}_{i-}||^{2H}) - 2N||\mathbf{k}||^{2H} \right)_{\mathbf{k}}\ast \Delta \\
&= -\frac{\sigma^2}{2}\left(\sum_{i=1}^N (||\mathbf{k}_{i+}||^{2H} + ||\mathbf{k}_{i-}||^{2H}) - 2N||\mathbf{k}||^{2H} \right)_{\mathbf{k}}\ast \Delta \\
&= -\frac{\sigma^2}{2}(||\mathbf{k}||^{2H})_{\mathbf{k}}\ast \Delta \ast\Delta.
\end{aligned}
$$
{{< /math >}}

## 离散 Fourier 变换

对于一维的带有周期边界条件的离散 Poisson 方程, 有
$$
{Y} = \Delta{B} = A{B}, \tag{5}
$$
其中 ${B}=(B_0, B_1, \cdots, B_{M-1})^T$, 边界 $B_0 = B_M$, 
{{< math >}}
$$
A =
\begin{bmatrix}
  -2 & 1 & 0 & \cdots & 0 & 0 & 1 \\
  1 & -2 & 1 & \cdots & 0 & 0 & 0 \\
  \vdots & \vdots  & \vdots & \cdots & \vdots & \vdots & \vdots  \\
  0 & 0 & 0 &\cdots & 1 & -2 & 1  \\
  1 & 0 & 0 &\cdots & 0 & 1 & -2
\end{bmatrix}
$$
{{< /math >}}
是一个循环矩阵, 则
$$
A = F^{-1} \Lambda F,
$$
其中 $F$ 是标准化的离散Fourier变换矩阵,  
{{< math >}}
$$
\Lambda = \mathrm{diag}\{g(\omega_0), \cdots, g(\omega_{M-1})\},
$$
{{< /math >}}
$g(x)=x^{M-1}+x-2$, $\omega_k = e^{i2\pi k/M}$, $k=0,1, \cdots, M-1$ 为 $M$ 次单位根.
{{< math >}}
$$
	\begin{aligned}
		g(\omega_k) &= \omega_k^{M-1} + \omega_k - 2 \\
		&= e^{i2\pi k(M-1)/M} + e^{i2\pi k/M} - 2 \\
		&= e^{i2\pi k}e^{-i2\pi k/M} + e^{i2\pi k/M} -2 \\
		&= e^{-i2\pi k/M} + e^{i2\pi k/M} -2 \\
		&= 2\cos{(2\pi k/M)} - 2\\
		&= -4 \sin^2{(2\pi k /(2M))}.
	\end{aligned}
$$
{{< /math >}}
对方程 (5) 进行离散 Fourier 变换, 得
$$
	\hat{{Y}} = F{Y} = FA{B} = FF^{-1}\Lambda F{B} = \Lambda \hat{{B}},
$$
所以分量
$$
	\hat{{Y}}_k = -4\sin^2{(2\pi k/(2M))}\hat{B}_k. 
$$

## 参考文献

Martin Dlask and  Jaromir Kukal, *Hurst exponent estimation of fractional surfaces for mammogram images analysis*, [Phys. A, **585** (2022) 126424](https://doi.org/10.1016/j.physa.2021.126424).

C. R. Dietrich and G. N. Newsam, *Fast and exact simulation of stationary Gaussian processes through circulant embedding of the covariance matrix*, [SIAM J. Sci. Comput., **18** (1997) 1088-1107](https://doi.org/10.1137/S1064827592240555). 