---
# Documentation: https://wowchemy.com/docs/managing-content/
reading_time: false
commentable: true
share: true
title: "欠(次)扩散方程, 积分变换与复合布朗运动"
subtitle: ""
summary: "利用 Laplace, Fourier, Mellin 等积分变换和复合布朗运动求解经典欠(次)扩散方程."
authors: []
tags: []
categories: ['XX','DONE']
date: 2023-08-27T18:48:50+08:00
lastmod: 2023-08-27T18:48:50+08:00
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

## 积分变换

> **定义** (拉普拉斯变换)
>设函数 $f(t)\in L^1([0,\infty); \mathbb{R})$, 并且存在常数 $C>0$ 以及 $\sigma\in \mathbb{R}$ 使得 $\vert f(t)\vert \sim C\mathrm{e}^{\sigma t}$, 则 $f(t)$ 的拉普拉斯变换 {{< math >}}$\widetilde{f}(s)=\mathscr{L}[f(t)](s)${{< /math >}} 定义为
{{< math >}}
$$\tilde{f}(s) = \int_0^{\infty}\mathrm{e}^{-st}f(t)\mathrm{d}s, \qquad \forall s\in \{z\in \mathbb{C}:\Re(z)>\sigma\}.$$
{{< /math >}}
称 {{< math >}}$\{z\in \mathbb{C}:\Re(z)>\sigma\}${{< /math >}} 为 $\tilde{f}(s)$ 的收敛域.
 
>**定义** (拉普拉斯逆变换) 函数 $\tilde{f}(s)$ 的拉普拉斯逆变换 {{< math >}}$f(t)=\mathscr{L}^{-1}[\tilde{f}(s)](t)${{< /math>}} 由如下复积分给出, 
{{< math >}}
$$
f(t) = \frac{1}{2\pi i}\int_{\gamma-i\infty}^{\gamma+i\infty}\mathrm{e}^{st}\tilde{f}(s)\mathrm{d}s,
$$
{{< /math >}}
其中 $\gamma\in\mathbb{R}$ 满足 {{< math >}}$\{z\in\mathbb{C}:\Re(z)=\gamma\}${{< /math >}} 包含在 $\tilde{f}$ 的收敛域内.

>**定义** (傅里叶变换)
设函数 $f(x)\in L^1(\mathbb{R}; \mathbb{R})$, 则 $f(x)$ 的傅里叶变换 {{< math >}}$\hat{f}(k)=\mathscr{F}[f(x)](k)${{< /math >}} 定义为
{{< math >}}
$$
\hat{f}(k) = \int_{\mathbb{R}}\mathrm{e}^{\mathrm{i}kx}f(x)\mathrm{d}x.
$$
{{< /math >}}

>**定义**(傅里叶逆变换) 函数 $\hat{f}(k)$ 的傅里叶逆变换 {{< math >}}$f(x)=\mathscr{F}^{-1}[\hat{f}(k)](x)${{< /math >}} 为
{{< math >}}
$$
f(x) = \frac{1}{2\pi}\int_{\mathbb{R}}\mathrm{e}^{-\mathrm{i}kx}\hat{f}(k)\mathrm{d}k.
$$
{{< /math >}}

>**定义**	(梅林变换) 设函数 $f(t):[0,\infty) \longrightarrow \mathbb{R}$, 则 $f(t)$ 的梅林变换 {{< math >}}$f^*(s)=\mathcal{M}[f(t)](s)${{< /math >}} 定义为
{{< math >}}
$$
f^*(s) = \int_{0}^{\infty}t^{s-1}f(t)\mathrm{d}t.
$$
{{< /math >}}

>**定义**	(梅林逆变换) 函数 {{< math >}}$f^{*}(s)${{< /math >}} 的梅林逆变换 {{< math >}}$f(t)=\mathcal{M}^{-1}[f^*(s)](t)${{< /math >}} 为
{{< math >}}
$$
f(t) = \frac{1}{2\pi \mathrm{i}}\int_{c-\mathrm{i}\infty}^{c+\mathrm{i}\infty}t^{-s}f^*(s)\mathrm{d}s,
$$
{{< /math >}}
其中 $c\in\mathbb{R}$ 满足 {{< math >}}$\{z\in\mathbb{C}:\Re(z)=c\}${{< /math >}} 包含在 $f^*$ 的解析区域内.

**性质1**	(拉普拉斯变换与梅林变换的关系)	
{{< math >}}
$$
\mathcal{M}\{\mathscr{L}[f(t)](s)\}(1-p) = \Gamma(1-p)\mathcal{M}[f(t)](p).
$$
{{< /math >}}
*Proof*.
{{< math >}}
\begin{equation}
\begin{aligned}
\mathcal{M}[\mathscr{L}[f(t)](s)](1-p) 
=&\int_{0}^{\infty}s^{-p}\int_0^{\infty}\mathrm{e}^{-st}f(t)\mathrm{d}t\mathrm{d}s \\
=&\int_0^{\infty}f(t)\int_0^{\infty}s^{-p}\mathrm{e}^{-st}\mathrm{d}s\mathrm{d}t \\
=&\int_{0}^{\infty}f(t)\int_{0}^{\infty}\left(\frac{z}{t}\right)^{-p}\mathrm{e}^{-z}\frac{\mathrm{d}z}{t}\mathrm{d}t  \qquad z=st \\
=&\Gamma(1-p)\int_0^{\infty}t^{p-1}f(t)\mathrm{d}t \\
=&\Gamma(1-p)\mathcal{M}[f(t)](p).
\end{aligned}
\end{equation}
{{< /math >}}

**性质2** (卷积的拉普拉斯变换) 函数 $f(t)$ 和 $g(t)$ 的卷积 $(f \ast g)(t)=\displaystyle\int_0^tf(t-\tau)g(\tau)\mathrm{d}\tau$ 的拉普拉斯变换
{{< math >}}
\begin{equation}
\mathscr{L}[f\ast g](s)=\mathscr{L}[f](s)\mathscr{L}[g](s).
\end{equation}
{{< /math >}}
*Proof*.
{{< math >}}
$$
\begin{aligned}
\mathscr{L}[f\ast g](s)
=&\int_{0}^{\infty}\mathrm{e}^{-st}\int_0^tf(t-\tau)g(\tau)\mathrm{d}\tau\mathrm{d}t \\
=&\int_0^{\infty}g(\tau)\int_{\tau}^{\infty}\mathrm{e}^{-st}f(t-\tau)\mathrm{d}t\mathrm{d}\tau \\
=&\int_0^{\infty}g(\tau)\int_0^{\infty}\mathrm{e}^{-s(u+\tau)}f(u)\mathrm{d}u\mathrm{d}\tau \qquad u=t-\tau \\
=&\left(\int_0^{\infty}\mathrm{e}^{-s\tau}g(\tau)\mathrm{d}\tau\right)\left(\int_0^{\infty}\mathrm{e}^{-su}f(u)\mathrm{d}u\right) \\
=&\mathscr{L}[f](s)\mathscr{L}[g](s).
\end{aligned}
$$
{{< /math >}}

**性质3** (导函数的拉普拉斯变换)
函数 $f(t)$ 的 $n$ 阶导函数 $f^{(n)}(t)$ 的拉普拉斯变换为
{{< math >}}
\begin{equation}
\mathscr{L}[f^{(n)}](s) = s^n\mathscr{L}[f](s) -\sum_{k=0}^{n-1}s^{n-1-k}f^{(k)}(0).
\end{equation}
{{< /math >}}
*Proof.*
{{< math >}}
\begin{equation*}
\begin{aligned}
\mathscr{L}[f^{(n)}](s)
=&\int_0^{\infty}\mathrm{e}^{-st}f^{(n)}(t)\mathrm{d}t \\
=&s\int_0^{\infty}\mathrm{e}^{-st}f^{(n-1)}(t)\mathrm{d}t - f^{(n-1)}(0) \\
=&s^n\int_0^{\infty}\mathrm{e}^{-st}f(t)\mathrm{d}t-\sum_{k=0}^{n-1}s^{n-1-k}f^{(k)}(0) \\
=&s^n\mathscr{L}[f](s) - \sum_{k=0}^{n-1}s^{n-1-k}f^{(k)}(0).
\end{aligned}
\end{equation*}
{{< /math >}}

**性质4**	(导函数的傅里叶变换) 速降函数 $f(x)$ 的 $n$ 阶导函数 $f^{(n)}(x)$ 的傅里叶变换为
{{< math >}}
\begin{equation}
\mathscr{F}[f^{(n)}](k) = (-\mathrm{i}k)^n\mathscr{F}[f](k).
\end{equation}
{{< /math >}}
*Proof.*
{{< math >}}
\begin{equation*}
\begin{aligned}
\mathscr{F}[f^{(n)}](k) 
=&\int_{\mathbb{R}}\mathrm{e}^{\mathrm{i}kx}f^{(n)}(x)\mathrm{d}x\\
=&-\mathrm{i}k\int_{\mathbb{R}}\mathrm{e}^{\mathrm{i}kx}f^{(n-1)}(x)\mathrm{d}x \\
=&(-\mathrm{i}k)^n\int_{\mathbb{R}}\mathrm{e}^{\mathrm{i}kx}f(x)\mathrm{d}x \\
=&(-\mathrm{i}k)^n\mathscr{F}[f](k).
\end{aligned}
\end{equation*}
{{< /math >}}

**性质5** (傅里叶变换及其逆变换的平移性质)
{{< math >}}
\begin{equation}
\mathscr{F}[f(x-x_0)](k) = \mathrm{e}^{\mathrm{i}kx_0}\mathscr{F}[f](k),
\end{equation}
\begin{equation}
\mathscr{F}^{-1}[\mathrm{e}^{\mathrm{i}kx_0}\mathscr{F}[f](k)](x) = f(x-x_0).
\end{equation}
{{< /math >}}
*Proof.*
{{< math >}}
\begin{equation*}
\begin{aligned}
\mathscr{F}[f(x-x_0)](k)
=&\int_{\mathbb{R}}\mathrm{e}^{\mathrm{i}kx}f(x-x_0)\mathrm{d}x \\
=&\int_{\mathbb{R}}\mathrm{e}^{\mathrm{i}k(x'+x_0)}f(x')\mathrm{d}x' \\
=&\mathrm{e}^{\mathrm{i}kx_0}\mathscr{F}[f](k).
\end{aligned}
\end{equation*}
{{< /math >}}

**例子** (幂函数的拉普拉斯变换) 设幂函数 $f(t)=t^{\alpha}$, 其中 $\alpha>-1$, 则
{{< math >}}
\begin{equation*}
\tilde{f}(s)= \int_0^{\infty}\mathrm{e}^{-st}t^{\alpha}\mathrm{d}t=\int_0^{\infty}\mathrm{e}^{-z}\left(\frac{z}{s}\right)^{\alpha}\frac{\mathrm{d}z}{s} = \frac{\Gamma(1+\alpha)}{s^{1+\alpha}}.
\end{equation*}
{{< /math >}}
**例子** ($\mathrm{e}^{-a\vert x\vert}$ 的傅里叶变换) 设 $f(x)=\mathrm{e}^{-a\vert x\vert}$, 其中 $a>0$, 则
{{< math >}}
\begin{equation}
\begin{aligned}
\mathscr{F}[f](k) &= \int_{\mathbb{R}}\mathrm{e}^{\mathrm{i}kx}\mathrm{e}^{-a\vert x\vert }\mathrm{d}x \\
=& \int_{\mathbb{R}}(\cos{(kx)}+\mathrm{i}\sin{(kx)})\mathrm{e}^{-a\vert x\vert}\mathrm{d}x \\
=& 2\int_0^{\infty}\cos{(kx)}\mathrm{e}^{-ax}\mathrm{d}x,
\end{aligned}
\end{equation}
{{< /math >}}
而
{{< math >}}
\begin{equation}
\begin{aligned}
&\int_0^{\infty}\cos{(kx)}\mathrm{e}^{-ax}\mathrm{d}x \\
=& \frac{1}{k}\int_0^{\infty}\mathrm{e}^{-ax}\mathrm{d}\sin{(kx)} \\
=&\frac{1}{k}\left[\mathrm{e}^{-ax}\sin{(kx)}\left.\right\vert_{x=0}^{x=\infty}+a\int_0^{\infty}\mathrm{e}^{-ax}\sin{(kx)}\mathrm{d}x\right] \\
=&\frac{a}{k}\int_0^{\infty}\mathrm{e}^{-ax}\sin{(kx)}\mathrm{d}x	\\
=&\frac{a}{k^2}	\left[-\mathrm{e}^{-ax}\cos{(kx)}\left.\right\vert_{x=0}^{x=\infty}-a\int_0^{\infty}\mathrm{e}^{-ax}\cos{(kx)}\mathrm{d}x\right] \\
=&\frac{a}{k^2}-\frac{a^2}{k^2}\int_0^{\infty}\cos{(kx)}\mathrm{e}^{-ax}\mathrm{d}x,
\end{aligned}
\end{equation}
{{< /math >}}
于是
{{< math >}}
\begin{equation}
\int_0^{\infty}\cos{(kx)}\mathrm{e}^{-ax}\mathrm{d}x = \frac{a}{k^2+a^2}.
\end{equation}
{{< /math >}}
所以
{{< math >}}
\begin{equation}
\mathscr{F}[f](k) =\frac{2a}{k^2+a^2}. 
\end{equation}
{{< /math >}}

## H 函数

>**定义** (H 函数) 设 $a_1$, $\cdots$, $a_p$, $b_1$, $\cdots$, $b_q \in \mathbb{C}$, $A_1$, $\cdots$, $A_p$, $B_1$, $\cdots$, $B_q > 0$, 则H 函数
{{< math >}}
\begin{equation}
\begin{aligned}
&H_{pq}^{mn} \left[\left. z  \right\vert_{(b1,B1),\cdots, (b_q, B_q)}^{(a_1, A_1), \cdots, (a_p,A_p)}\right]\\
=&\frac{1}{2\pi i}\int_{c-\mathrm{i}\infty}^{c+\mathrm{i}\infty}\frac{\prod\limits_{i=1}^{m}\Gamma(b_i+B_is)\prod\limits_{i=1}^n\Gamma(1-a_i-A_is)}{\prod\limits_{i=n+1}^{p}\Gamma(a_i+A_is)\prod\limits_{i=m+1}^q\Gamma(1-b_i-B_is)}z^{-s}\mathrm{d}s.
\end{aligned}
\end{equation}
{{< /math >}}
	
**例子** 设函数 $f(t)$ 的拉普拉斯变换 $\tilde{f}(s)=s^{\mu}\mathrm{e}^{-as^{\nu}}$, 其中 $a>0$, 求 $f(t)$.

首先利用梅林变换和拉普拉斯变换的关系, 可以得到
{{< math >}}
\begin{equation}
\Gamma(1-p)\mathcal{M}[f](p) = \int_0^{\infty}s^{-p}s^{\mu}\mathrm{e}^{-as^{\nu}}\mathrm{d}s.
\end{equation}  
{{< /math >}}
对上式积分进行变量替换 $z = as^{\nu}$, $s = (z/a)^{1/\nu}$, $\mathrm{d}s = (z/a)^{1/\nu-1}/(a\nu)\mathrm{d}z$ 可得
{{< math >}}
\begin{equation}
\begin{aligned}
\mathcal{M}[f](p) &= \frac{1}{\Gamma(1-p)}\int_0^{\infty}\frac{1}{a\nu}\left(\frac{z}{a}\right)^{\frac{\mu-p}{\nu}}\left(\frac{z}{a}\right)^{\frac{1}{\nu}-1}\mathrm{e}^{-z}\mathrm{d}z \\
&=\frac{1}{\Gamma(1-p)}\frac{1}{\nu a^{\frac{\mu+1-p}{\nu}}}\int_0^{\infty}z^{\frac{\mu+1-p}{\nu}-1}\mathrm{e}^{-z}\mathrm{d}z \\
&=\frac{1}{\nu a^{\frac{\mu+1-p}{\nu}}}\frac{\Gamma(\frac{\mu+1-p}{\nu})}{\Gamma(1-p)}.
\end{aligned}
\end{equation}
{{< /math >}}
所以
{{< math >}}
\begin{equation}
\begin{aligned}
f(t) &= \frac{1}{\nu a^{\frac{\mu+1}{\nu}}}\frac{1}{2\pi \mathrm{i}}\int_{c-\mathrm{i}\infty}^{c+\mathrm{i}\infty}\frac{\Gamma(\frac{\mu+1-s}{\nu})}{\Gamma(1-s)}\left(\frac{t}{a^{\frac{1}{\nu}}}\right)^{-s}\mathrm{d}s  \\
&=\frac{1}{\nu a^{\frac{\mu+1}{\nu}}}\frac{1}{2\pi \mathrm{i}}\int_{c-\mathrm{i}\infty}^{c+\mathrm{i}\infty}\frac{\Gamma(\frac{\mu+1+s}{\nu})}{\Gamma(1+s)}\left(\frac{a^{\frac{1}{\nu}}}{t}\right)^{-s}\mathrm{d}s \\
&= \frac{1}{\nu a^{\frac{\mu+1}{\nu}}}H_{11}^{10}\left[\left.\frac{a^{\frac{1}{\nu}}}{t}\right\vert_{(\frac{\mu+1}{\nu}, \frac{1}{\nu})}^{(1,1)} \right].
\end{aligned}
\end{equation}
{{< /math >}}
进一步, 可利用留数定理对上述积分进行展开. 对于伽马函数 $\Gamma(z)$ 而言, $\Gamma(n)=\infty$, $n=0$, $-1$, $-2$, $\cdots$, 并且奇点只有一阶极点 $\{0, -1, -2, \cdots\}$, 所以上述积分的被积函数的奇点, 即一阶极点为 $(\mu+1+s_n)/\nu = -n$, $s_n = -1 - \mu - \nu n$, $n=0$, $1$, $2$, $\cdots$, 于是留数
{{< math >}}
\begin{equation}	
\begin{aligned}
\textnormal{Res}(s_n) &= \lim_{s\to s_n}(s-s_n)\frac{\Gamma\left(\frac{\mu+1+s}{\nu}\right)}{\Gamma(1+s)}\left(\frac{a^{\frac{1}{\nu}}}{t}\right)^{-s} \\
&= \frac{1}{\Gamma(-\mu-\nu n)}\left(\frac{a^{\frac{1}{\nu}}}{t}\right)^{1+\mu+\nu n} \lim_{s\to s_n}(s-s_n)\Gamma\left(\frac{\mu+1+s}{\nu}\right) \\
&= \frac{\nu}{n!\Gamma(-\mu-\nu n)}\left(\frac{a^{\frac{1}{\nu}}}{t}\right)^{1+\mu}\left(-\frac{a}{t^{\nu}}\right)^{n},
\end{aligned}
\end{equation}
{{< /math >}}
这是因为
{{< math >}}
$$
\begin{aligned}
&\lim_{s\to s_n}(s-s_n)\Gamma\left(\frac{\mu+1+s}{\nu}\right)\\
=&\lim_{s\to -1-\mu - \nu n}(s+1+\mu+\nu n)\Gamma\left(\frac{\mu+1+s}{\nu}\right) \\
=& \lim_{s\to -1-\mu-\nu n}\frac{(s+1+\mu+\nu n)\Gamma\left(\frac{\mu+1+s}{\nu}+1\right)}{\frac{\mu+1+s}{\nu}}\\
=& \lim_{s\to -1-\mu-\nu n}\frac{(s+1+\mu+\nu n)\Gamma\left(\frac{\mu+1+s}{\nu}+n+1\right)}{\frac{\mu+1+s}{\nu}\cdots\left(\frac{\mu+1+s}{\nu}+n\right)} \\
=& \lim_{s\to -1-\mu-\nu n}\frac{\Gamma\left(\frac{\mu+1+s}{\nu}+n+1\right)}{\frac{\mu+1+s}{\nu}\cdots\left(\frac{\mu+1+s}{\nu}+n-1\right)}\nu \\
=&\frac{\nu}{(-n)\cdots (-1)} \\
=&\frac{(-1)^n\nu}{n!}.
\end{aligned}
$$
{{< /math >}}
所以 $f(t)$ 还可以表示为下述形式
{{< math >}}
\begin{equation}
f(t) = \frac{1}{t^{1+\mu}}\sum_{n=0}^{\infty}\frac{1}{n!\Gamma(-\mu-\nu n)}\left(-\frac{a}{t^{\nu}}\right)^{n}.
\end{equation}
{{< /math >}}
于是, 若定义 Mainardi 函数如下,
{{< math >}}
\begin{equation}
f_{\mu,\nu}(t;a)=\frac{1}{t^{1+\mu}}\sum_{n=0}^{\infty}\frac{1}{n!\Gamma(-\mu-\nu n)}\left(-\frac{a}{t^{\nu}}\right)^{n},
\end{equation}
{{< /math >}}
那么
{{< math >}}
\begin{equation}
\mathscr{L}^{-1}\{s^{\mu}\mathrm{e}^{-as^{\nu}}\}(t)=f_{\mu,\nu}(t; a).
\end{equation}
{{< /math >}}
 	
## 分数阶积分和导数

>**定义** ($\alpha$ 阶 Riemann-Liouville 积分) 设函数 $f(t)\in L^1(a,b)$, $\alpha>0$, 则 $f(t)$ 的 $\alpha$ 阶 Riemann-Liouville 积分 {{< math >}}$ ({}_{a}I_t^{\alpha}f)(t)${{< /math >}} 定义为
{{< math >}}
\begin{equation}
({}_{a}I_t^{\alpha}f)(t) = \frac{1}{\Gamma(\alpha)}\int_a^t(t-s)^{\alpha-1}f(s)ds.
\end{equation}
{{< /math >}}

>**定义** ($\alpha$ 阶 Caputo 导数) 设 $\alpha>0$, $n=[\alpha]+1$, 函数 $f(t)\in C^n(a,b)$, 则 $f(t)$ 的 $\alpha$ 阶 Caputo 导数$({}_a^CD_t^{\alpha}f)(t)$ 定义为
{{< math >}}
\begin{equation}
\begin{aligned}
({}_a^CD_t^{\alpha}f)(t) &= \left({}_aI_t^{n-\alpha}\frac{d^n}{dt^n}\right)f(t)\\
& = \frac{1}{\Gamma(n-\alpha)}\int_a^t(t-s)^{n-\alpha-1}f^{(n)}(s)\mathrm{d}s.
\end{aligned}
\end{equation}
{{< /math >}}

**性质6** (Caputo 导数的拉普拉斯变换)
由上述卷积和导函数的拉普拉斯变换, $({}_0^CD_t^{\alpha}f)(t)$ 的拉普拉斯变换为
{{< math >}}
\begin{equation}
\mathscr{L}[({}_0^CD_t^{\alpha}f)(t)](s) = s^{\alpha}\mathscr{L}[f](s) - \sum_{k=0}^{n-1}s^{\alpha-1-k}f^{(k)}(0).
\end{equation}
{{< /math >}}

## 从属过程(subodinator)

>**定义** ($\alpha$-稳定 从属过程) 称随机过程 $T(t)$ 是一个 $\alpha$-稳定的从属过程, 如果它是一个非减的 $\alpha$-稳定 的 Lévy 过程.

**性质7** (拉普拉斯指数) 设 $T(t)$ 是一个$ \alpha$-稳定的从属过程, 则其拉普拉斯指数为 $-s^{\alpha}$, 即
{{< math >}}
\begin{equation}
\tilde{g}(s,t) = \mathbb{E}\mathrm{e}^{-sT(t)}=\int_0^{\infty}\mathrm{e}^{-sT}g(x,t)\mathrm{d}T = \mathrm{e}^{-ts^{\alpha}},
\end{equation}
{{< /math >}}
其中 $g(x,t)$ 是 $T(t)$ 的概率密度函数.

**性质8** (scaling property) 设 $T(t)$ 是一个 $\alpha$-稳定的从属过程, 则
{{< math >}}
\begin{equation}
T(t) \overset{\mathrm{d}}{=} t^{1/\alpha}T(1).
\end{equation}
{{< /math >}}
*Proof.*
{{< math >}}
\begin{equation*}
\mathbb{E}\mathrm{e}^{-sT(t)}=\mathrm{e}^{-ts^{\alpha}}=\mathrm{e}^{-1\dot (t^{1/\alpha}s)^{\alpha}} = \mathbb{E}\mathrm{e}^{-(t^{1/\alpha}s)T(1)}.
\end{equation*}
{{< /math >}}
由上述性质, 可以得到
{{< math >}}
\begin{equation}
\begin{aligned}
g(x,t) &= \partial_x\int_{0}^xg(u,t)\mathrm{d}u \\
&= \partial_x \mathbb{P}(T(t)\leqslant x) \\
&= \partial_x \mathbb{P}(t^{1/\alpha}T(1)\leqslant x)\\
&= \partial_x \mathbb{P}(T(1)\leqslant t^{-1/\alpha}x) \\
&= \partial_x \int_0^{t^{-1/\alpha}x}g_{\alpha}(u)\mathrm{d}u \\
&= t^{-1/\alpha}g_{\alpha}(t^{-1/\alpha}x),
\end{aligned}
\end{equation}
{{< /math >}}
其中 $g_{\alpha}(x)$ 为 $T(1)$ 的概率密度函数, 其拉普拉斯变换为 $\tilde{g}_{\alpha}(s)=\mathrm{e}^{-s^{\alpha}}$. 进一步,  
{{< math >}}
\begin{equation}
g_{\alpha}(x) =\frac{1}{\alpha} H\left[\frac{1}{x}\left.\right\vert_{(\frac{1}{\alpha}, \frac{1}{\alpha})}^{(1,1)} \right].
\end{equation}
{{< /math >}}

## 逆从属过程

>**定义** (逆从属过程) 设 $T(t)$ 是一个 $\alpha$-稳定从属过程, 则逆从属过程 $E(t)$ 是 $T(t)$ 的逆过程, 即
{{< math >}}
\begin{equation}
E(t) = \inf\{u>0:T(u)>t\}.
\end{equation}
{{< /math >}}

设 $h(u,t)$ 是 $E(t)$ 的概率密度函数, 则根据定义, 有
{{< math >}}
\begin{equation}
\begin{aligned}
h(u,t) &=\partial_u \mathbb{P}(E(t)\leqslant u) \\
&=\partial_u \mathbb{P}(T(u)\geqslant t) \\
<!-- &=\partial_u(1-\mathbb{P}(T(u)<t))\\ -->
&=-\partial_u \int_0^t g(x,u)\mathrm{d}x \\
&=-\partial_u \int_0^t u^{-1/\alpha}g_{\alpha}(u^{-1/\alpha}x)\mathrm{d}x \\
&=-\partial_u\int_0^{u^{-1/\alpha}t}g_{\alpha}(y)\mathrm{d}y \qquad y=u^{-1/\alpha}x \\
&= \frac{t}{\alpha}u^{-1-1/\alpha}g_{\alpha}(u^{-1/\alpha}t) \\
&=\frac{t}{\alpha^2}u^{-1-1/\alpha}H\left[\frac{u^{1/\alpha}}{t}\left.\right\vert_{(\frac{1}{\alpha}, \frac{1}{\alpha})}^{(1,1)} \right],
\end{aligned}
\end{equation}
{{< /math >}}
{{< math >}}
\begin{equation}
\tilde{h}(u,s) = -\partial_u \frac{\tilde{g}(s,u)}{s}=-\partial_u s^{-1}\mathrm{e}^{-us^{\alpha}}=s^{\alpha-1}\mathrm{e}^{-us^{\alpha}}.
\end{equation}
{{< /math >}}	

## 欠扩散方程

欠扩散方程
{{< math >}}
\begin{equation}\tag{EQ}\label{eq}
\partial_t^{\alpha}P(x,t) = D\partial_x^2P(x,t),\qquad
P(x,0)=\delta(x-x_0).
\end{equation}
{{< /math >}}
其中 $\partial_t^{\alpha}={}_0D_t^{\alpha}$ 是 Caputo 导数, $0<\alpha<1$, $D$ 为扩散系数. 

对方程两边做拉普拉斯-傅里叶变换, 得
{{< math >}}
\begin{equation}
s^{\alpha}\hat{\tilde{P}}(k,s)-\mathrm{e}^{\mathrm{i}kx_0}s^{\alpha-1} = -Dk^2\hat{\tilde{P}}(k,s),
\end{equation}
{{< /math >}}
即
{{< math >}}
\begin{equation}
\hat{\tilde{P}}(k,s)= \frac{\mathrm{e}^{\mathrm{i}kx_0}s^{\alpha-1}}{s^{\alpha}+Dk^2}.
\end{equation}
{{< /math >}}
根据上面的例子, 有
{{< math >}}
\begin{equation}
\tilde{P}(x,s) = \frac{1}{2\sqrt{D}s^{1-\alpha/2}}\mathrm{e}^{-\frac{s^{\alpha/2}}{\sqrt{D}}\vert x-x_0\vert},
\end{equation}
\begin{equation}
\begin{aligned}
P(x,t) &= \frac{1}{\alpha\vert x-x_0\vert}H_{11}^{10}\left[\left.{\left(\frac{\vert x-x_0\vert}{\sqrt{D}}\right)^{2/\alpha}}
{t^{-1}}\right\vert_{(1,\frac{2}{\alpha})}^{(1,1)}\right] \\
&=\frac{1}{2\sqrt{D}}f_{-1+\alpha/2, \alpha/2}\left(t;\frac{|x-x_0|}{\sqrt{D}} \right).
\end{aligned}
\end{equation}
{{< /math >}}

$\alpha=1$ 时, 我们有
{{< math >}}
\begin{align}
P(x,t) &= \frac{1}{2\sqrt{D}}f_{-1/2, 1/2}\left(t;\frac{|x-x_0|}{\sqrt{D}} \right)\\
&=\frac{1}{2\sqrt{D}}\frac{1}{t^{1/2}}\sum_{n=0}^{\infty}\frac{1}{n!\Gamma(1/2-(1/2)n)}\left(-\frac{|x-x_0|}{\sqrt{D}}\frac{1}{t^{1/2}}\right)^n \\
&=\frac{1}{\sqrt{4Dt}}\sum_{n=0}^{\infty}\frac{1}{n!\Gamma((1-n)/2)}\left(-\frac{|x-x_0|}{\sqrt{Dt}}\right)^n.
\end{align}
{{< /math >}}
因为当 $n$ 为奇数时, $1/\Gamma((1-n)/2)=0$, 所以
{{< math >}}
\begin{align}
P(x,t)&=\frac{1}{\sqrt{4Dt}}\sum_{n=0}^{\infty}
\frac{1}{(2n)!\Gamma((1-2n)/2)}\left(-\frac{|x-x_0|}{\sqrt{Dt}}\right)^{2n}\\
&=\frac{1}{\sqrt{4Dt}}\sum_{n=0}^{\infty}
\frac{1}{(2n)!\Gamma(1/2-n)}\left(\frac{|x-x_0|^2}{{Dt}}\right)^{n}.
\end{align}
{{< /math >}}
又因为
{{< math >}}
\begin{align}
&\Gamma(1/2-n)\\
=&\frac{\Gamma{(1/2-n+1)}}{1/2-n} \\
=& \frac{\Gamma{(1/2-n+n)}}{(1/2-n)(1/2-n+1)\cdots(1/2-n+n-1)}  \\
=& \frac{\Gamma(1/2)(-2)^n}{1\times 3\times\cdots\times(2n-1)} \\
=& \frac{\sqrt{\pi}(-2)^n}{(2n-1)!!},
\end{align}
{{< /math >}}
所以
{{< math >}}
\begin{align}
\frac{1}{(2n)!\Gamma{(1-n/2)}}
=&\frac{(2n-1)!!}{\sqrt{\pi}(2n)!(-2)^n}\\
=&\frac{1}{\sqrt{\pi}(2n)!!(-2)^n}\\
=&\frac{1}{\sqrt{\pi}(n!2^n)(-2)^n}\\
=&\frac{1}{\sqrt{\pi}n!(-4)^n},
\end{align}
{{< /math >}}
于是
{{< math >}}
\begin{align}
P(x,t)&=\frac{1}{\sqrt{4Dt}}\sum_{n=0}^{\infty}\frac{1}{\sqrt{\pi}n!(-4)^n}\left(\frac{|x-x_0|^2}{Dt}\right)^n\\
&=\frac{1}{\sqrt{4\pi Dt}}\sum_{n=0}^{\infty}\frac{1}{n!}\left(-\frac{|x-x_0|^2}{4Dt}\right)^n
\\
&=\frac{1}{\sqrt{4\pi Dt}}\mathrm{e}^{-\frac{(x-x_0)^2}{4Dt}}.
\end{align}
{{< /math >}}
	
## 复合布朗运动

假设方程 ($\ref{eq}$) 的解 $P(x,t)$ 具有如下形式
{{< math >}}
\begin{equation}\tag{C}\label{c}
P(x,t) = \int_0^{\infty}n(s,t)P_0(x,s)\mathrm{d}x,
\end{equation}
{{< /math >}}
其中 $P_0(x,t)$ 是扩散方程
{{< math >}}
\begin{equation}
\partial_t P_0(x,t) = D\partial_x^2P_0(x,t),
\qquad
P_0(x,0)=\delta(x-x_0),
\end{equation}
{{< /math >}}
的解.
下面说明 $n(s,t)$ 就是前面所说的逆从属过程的概率密度函数, 即 $h$.

首先对 ($\ref{c}$) 式两边对 $x$ 积分, 然后进行拉普拉斯变换 $t\to u$, 得
{{< math >}}
\begin{equation}
\int_{\mathbb{R}}P(x,t)\mathrm{d}x  = \int_0^{\infty}n(s,t)\int_{\mathbb{R}}P_0(x,s)\mathrm{d}x\mathrm{d}s,
\end{equation}
\begin{equation}
1 = \int_0^{\infty}n(s,t)\mathrm{d}s,
\end{equation}
\begin{equation}
\frac{1}{u} = \int_0^{\infty}\tilde{n}(s,u)\mathrm{d}s.
\end{equation}
{{< /math >}}
对方程 ($\ref{eq}$) 进行拉普拉斯变换, 得
{{< math >}}
\begin{equation}
u\tilde{P}(x,u)-\delta(x-x_0)=Du^{1-\alpha}\partial_x^2\tilde{P}(x,u),
\end{equation}
\begin{equation}
\begin{aligned}
&u\int_{0}^{\infty}\tilde{n}(s,u)P_0(x,s)\mathrm{d}s - \delta(x-x_0)\\
=&Du^{1-\alpha}\int_0^{\infty}\tilde{n}(s,u)\partial_x^2P_0(x,s)\mathrm{d}s\\
=&u^{1-\alpha}\int_0^{\infty}\tilde{n}(s,u)\partial_s P_0(x,s)\mathrm{d}s \\
=&u^{1-\alpha}\left(\tilde{n}(s, u)P_0(x,s)|_{s=0}^{s=\infty}-\int_{0}^{\infty}\partial_s\tilde{n}(s,u)P_0(x,s)\mathrm{d}s\right),
\end{aligned}
\end{equation}
{{< /math >}}
其中, $\tilde{n}(\infty,u)=0$, $P_0(x,\infty)$ 是经典热扩散方程的稳态解, 即 Boltzmann 分布.
所以上式就可以写作
{{< math >}}
\begin{equation}
\begin{aligned}
&\int_0^{\infty}\left(u\tilde{n}(s,u)+u^{1-\alpha}\partial_s\tilde{n}(s,u)\right)P_0(x,s)\mathrm{d}s\\
=& \left(1-u^{1-\alpha}\tilde{n}(0,u)\right)\delta(x-x_0),
\end{alignedw}
\end{equation}
{{< /math >}}
要想这个式子成立, 只能是两边都为零, 即
{{< math >}}
\begin{equation}
\partial_s\tilde{n}(s,u) = -u^{\alpha}\tilde{n}(s,u),
\end{equation}
\begin{equation}
\tilde{n}(0,u)=u^{\alpha-1},
\end{equation}
{{< /math >}}
解之得
{{< math >}}
\begin{equation}
\tilde{n}(s,u) = u^{\alpha-1}\mathrm{e}^{-u^{\alpha}s}.
\end{equation}
{{< /math >}}
这个和 $\tilde{h}$ 是一样的, 所以说 $n$ 是逆从属过程的概率密度, 即欠扩散方程 ($\ref{eq}$) 是复合布朗运动 $B(E(t))$ 所对应的扩散方程.
