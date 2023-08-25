---
# Documentation: https://wowchemy.com/docs/managing-content/
commentable: true
share: true
title: "Langevin 方程与 Fokker-Planck 方程"
subtitle: ""
summary: "过阻尼 Langevin 方程所对应的 Fokker-Planck 方程"
authors: []
tags: []
categories: ['XX']
date: 2023-08-24T21:24:08+08:00
lastmod: 2023-08-24T21:24:08+08:00
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
## 过阻尼 Langevin 方程

描述粒子运动位置随时间演化的过阻尼 Langevin 方程为
{{< math >}}
$$
\frac{\mathrm{d}x(t)}{\mathrm{d}t} = f(x(t),t)+g(x(t), t)\xi(t),\tag{1}\label{1}
$$
{{< /math >}}
其中 $x(t)$ 是粒子 $t$ 时刻的位置, $f(x,t)$ 是外部力, $g(x,t)$ 是乘性噪声项, $\xi(t)$ 是系统的随机力 (噪声), 这里设 $\xi(t)$ 为布朗运动 $B(t)$ 生成的高斯白噪声, 其满足
{{< math >}}
$$
\langle \xi(t)\rangle = 0, \qquad 
\langle \xi(t)\xi(t')\rangle = 2D\delta(t-t'),
$$
{{< /math >}}
这里 $D$ 为布朗运动的扩散系数, $\delta(\cdot)$ 为 Dirac delta 函数. 
此外, 我们知道布朗运动 $B(t)\sim\mathcal{N}(0,2Dt)$, 且具有独立增量性和平稳增量性:
{{< math >}}
$$
B(t+\tau)-B(t)\sim\mathcal{N}(0, 2D\tau).
$$
{{< /math >}}

## 推导方法1

$n$ 阶 Kramer-Moyal 系数定义为
{{< math >}}
$$
D_n = \frac{1}{n!}\lim_{\tau\to 0}\left.\frac{1}{\tau}M_n(t)\right|_{x(t)=x} = \frac{1}{n!}\lim_{\tau\to 0}\left.\frac{\langle (x(t+\tau)-x(t))^n\rangle }{\tau}\right|_{x(t)=x}.
$$
{{< /math>}}
为了求 $x(t)$ 的 Kramer-Moyal 系数, 首先, 对方程 $\eqref{1}$ 积分, 得
{{< math >}}
$$
x(t+\tau)-x = \int_{t}^{t+\tau}f(x(s),s)\mathrm{d}s+\int_{t}^{t+\tau}g(x(s),s)\mathrm{d}B(s).
$$
{{< /math >}}
记增量 $w(\tau)=B(t+\tau)-B(t)$, 我们有
{{< math >}}
$$
\langle w(\tau)\rangle =0,\qquad \langle w(\tau_1)w(\tau_2)\rangle = 2D\min\{\tau_1,\tau_2\}.
$$
{{< /math >}}
然后对函数 $f$ 和 $g$ 在 $x$ 点处展开, 则
{{< math >}}
$$
\begin{aligned}
x(t+\tau)-x =& \int_{t}^{t+\tau}f(x,s)\mathrm{d}s + \int_{t}^{t+\tau}(x(s)-x)f_x^{'}(x,s)\mathrm{d}s \\
+& \frac{1}{2!}\int_{t}^{t+\tau}(x(s)-x)^2f_{xx}^{''}(x,s)\mathrm{d}s + \cdots  \\
+&\int_{t}^{t+\tau}g(x,s)\mathrm{d}B(s) + \int_{t}^{t+\tau}(x(s)-x)g_x^{'}(x,s)\mathrm{d}B(s) \\
+& \frac{1}{2!}\int_{t}^{t+\tau}(x(s)-x)^2g_{xx}^{''}(x,s)\mathrm{d}B(s) + \cdots.
\end{aligned}
$$
{{< /math >}}
根据上式, 又有
{{< math >}}
$$
\begin{aligned}
x(s)-x =& \int_{t}^{s}f(x,\xi)\mathrm{d}\xi + \int_{t}^{s}(x(\xi)-x)f_x^{'}(x,\xi)\mathrm{d}\xi \\
+& \frac{1}{2!}\int_{t}^{s}(x(\xi)-x)^2f_{xx}^{''}(x,\xi)\mathrm{d}\xi + \cdots  \\
+&\int_{t}^{s}g(x,\xi)\mathrm{d}B(\xi) + \int_{t}^{s}(x(\xi)-x)g_x^{'}(x,\xi)\mathrm{d}B(\xi) \\
+& \frac{1}{2!}\int_{t}^{s}(x(\xi)-x)^2g_{xx}^{''}(x,\xi)\mathrm{d}B(\xi) + \cdots.
\end{aligned}
$$
{{< /math >}}
重新代入, 得
{{< math >}}
$$
\begin{aligned}
x(t+\tau)-x =& \int_t^{t+\tau}f(x,s)\mathrm{d}s + \int_t^{t+\tau}f_x^{'}(x,s)\int_t^sf(x,\xi)\mathrm{d}\xi\mathrm{d}s \\
+& \int_{t}^{t+\tau}f_x^{'}(x,s)\int_{t}^sg(x,\xi)\mathrm{d}B(\xi)\mathrm{d}s\\
+& \int_t^{t+\tau}g(x,s)\mathrm{d}B(s) + \int_t^{t+\tau}g_x^{'}(x,s)\int_t^sf(x,\xi)\mathrm{d}\xi\mathrm{d}B(s) \\
+&\int_{t}^{t+\tau}g_x^{'}(x,s)\int_{t}^sg(x,\xi)\mathrm{d}B(\xi)\mathrm{d}B(s)+\cdots.
\end{aligned}
$$
{{< /math >}}
于是,
{{< math >}}
$$
\begin{aligned}
D_1(x,t)=&\lim_{\tau\to0}\frac{1}{\tau}\left(\int_t^{t+\tau}f(x,s)\mathrm{d}s + \int_t^{t+\tau}f_x^{'}(x,s)\int_t^sf(x,\xi)\mathrm{d}\xi\mathrm{d}s\right. \\
&\qquad\qquad\left.+\int_{t}^{t+\tau}g_x^{'}(x,s)\int_{t}^sg(x,\xi)\mathrm{d}B(\xi)\mathrm{d}B(s)\right) \\
=& f(x,t)+g_x^{'}(x,t)g(x,t)\lim_{\tau\to 0}\frac{1}{\tau}\left\langle\int_0^{\tau}w(s)\mathrm{d}w(s) \right\rangle \\
=& f(x,t),
\end{aligned}
$$
$$
\begin{aligned}
D_2(x,t) &= \frac{1}{2}\lim_{\tau\to 0}\frac{1}{\tau}\left\langle \int_{t}^{t+\tau}g(x,s)\mathrm{d}B(s)\int_t^{t+\tau}g(x,s)\mathrm{d}B(s) \right\rangle\\
&=\frac{g^2(x,t)}{2}\lim_{\tau\to0}\frac{1}{\tau}\langle w^2(\tau)\rangle \\
&= Dg^2(x,t).
\end{aligned}
$$
{{< /math >}}

