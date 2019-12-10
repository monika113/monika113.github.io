---
layout:     post
title:      RKHS 再生核希尔伯特空间
subtitle:   
date:       2019-12-10
author:     monika113
header-img: img/post-bg-cook.jpg
catalog: true
tags:
    - math
    - machine learning
    - TCA
---

再生核希尔伯特空间 reproducing kernel Hilbert space (RKHS) 在机器学习中很常见，比如Transfer Learning里的经典方法TCA。

## HS 希尔伯特空间
希尔伯特空间$\mathcal{H}$是指具有如下两个性质的空间：
1. 内积：$<\cdot,\cdot>: \mathcal{H}\times\mathcal{H}\rightarrow \mathbb{R}$.
2. 完备性：所有柯西序列都收敛，且极限在$\mathcal{H}$中。

## Kernel 核
$\mathcal{X}$是一个集合，比如样本集，$\mathcal{X}$上可能没有内积，也可能内积不是我们想要的（比如SVM，样本集本身线性不可分）。这时我们讲$\mathcal{X}$映射到一个高维的Hilbert空间中$\phi:\mathcal{X}\rightarrow \mathcal{H}$.

核函数$k: \mathcal{X}\times \mathcal{X} \rightarrow \mathbb{R}$:
$$
<x,y>_k = <\phi(x),\phi(y)>_\mathcal{H}
$$

## reproducing kernel 再生核
reproducing kernel 满足以下两个条件：
1. $\forall x\in \mathcal{X},k(\cdot, x)\in\mathcal{H}$
2. $\forall x\in \mathcal{X},f\in \mathcal{H}, <f(\cdot),k(\cdot,x)>_\mathcal{H}=f(x)$

这里有一个比较难理解的点，$k(\cdot,x)$是一个从$\mathcal{X}$到$\mathbb{R}$的函数，为什么可以说它属于$\mathcal{H}$?

事实上，$\mathcal{H}$与函数空间$\mathcal{F}=\{f:\mathcal{X}\rightarrow \mathbb{R}\}$的一个子空间是同构的。

具体证明写起来比较麻烦，主要的逻辑是固定一个$x_{0}$，对于任意$h\in\mathcal{H}$，都存在$\phi_h:\mathcal{X}\rightarrow \mathbb{R},s.t.\phi_h(x)=h$，那么由$\phi_h$可以得到一个核函数$k(x,y) = <\phi_h(x),\phi_h(y)>_\mathcal{H}$。取$x=x_{0}$，可以得到一个由$\mathcal{X}$到$\mathbb{R}$的函数$f(y)=k(x_0,y)=<h,\phi_h(y)>_\mathcal{H}$。

上述只是一个基本思路，还要证明这样的映射关系是同构的，属于抽象代数的范畴了，等我有时间再来补。

## RKHS
拥有再生核的Hilbert空间就是RKHS啦。注意，Hilbert空间是一个独立的概念，只和该空间自身的性质有关，但是RKHS不仅与其自身有关，还与$\mathcal{X}$有关。

另一种定义的方法更偏抽象代数一点：对于任意一个函数$f:\mathcal{X}\rightarrow \mathbb{R}$，我们可以将它看作是一个二元函数$\rho:\mathcal{F}\times\mathcal{X}\rightarrow \mathbb{R}$，$\rho(f,x)=f(x)$。对于固定的某个$x$，$\rho_x$是从$\mathcal{F}$到$\mathcal{X}$的映射，$\rho_x(f) =f(x)$。
由于$\mathcal{H}$是$\mathcal{F}$的子空间，我们也可以在$\mathcal{H}$上定义$\rho_x$。

$\mathcal{H}$是RKHS，若对任意$x\in\mathcal{X}$，存在$\lambda_x$，s.t.
$$
|\rho_x(f)|\leq\lambda_x||f||_\mathcal{H}
$$


## RKHS的应用

在用TCA做迁移学习的时候，两个domain的分布间的距离是由MMD来衡量的。关于Maximum mean discrepancy(MMD)[[Borgwardt et al., 2006]](https://doi.org/10.1093/bioinformatics/btl242) 里为什么要将样本空间映射到一个RKHS上，应用了什么性质。我们放到TCA的文章里去讲。