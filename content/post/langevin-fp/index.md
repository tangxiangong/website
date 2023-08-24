---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Langevin 方程与 Fokker-Planck 方程"
subtitle: ""
summary: "过阻尼 Langevin 方程所对应的 Fokker-Planck 方程"
authors: []
tags: []
categories: ['For X', '笔记']
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

### Kramer-Moyal 系数
