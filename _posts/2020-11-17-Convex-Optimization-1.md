---
layout:     post
title:      Convex Optimization 1
subtitle:   终于开始自学优化了（所以我为什么不听课呢
date:       2020-11-17
author:     Yue
header-img: img/palace.jpg
catalog: true
tags:
    - optimization
    - notes
---

## Some notes about concepts I always forget

1. convex set凸集

   ![image-20201117215047435](2020-11-17-Convex-Optimization-1.assets/image-20201117215047435.png)

2. convex function凸函数

   ![image-20201117215119009](2020-11-17-Convex-Optimization-1.assets/image-20201117215119009.png)

3. convex combination凸组合

4. convex hull凸包

5. cone锥

6. convex cone凸锥

7. conic combination锥组合

8. conic hull

   ![image-20201118110156234](2020-11-17-Convex-Optimization-1.assets/image-20201118110156234.png)

   ![image-20201118110223557](2020-11-17-Convex-Optimization-1.assets/image-20201118110223557.png)

9. affine transformation仿射变换

   ![affine transformations](https://s2.ax1x.com/2019/05/30/VKWszD.png)

   仿射变换包括以上所有变换，及这些变换任意次序、次数的组合。

   ![transformations venn diagram](https://s2.ax1x.com/2019/05/30/VKWwIx.png)

## Convex optimization problems

### 1. optimization problem

$$
min_{x\in D}f(x)\\
\begin{align}
subject \quad to \quad &g_i(x) \le0,\quad i=1,...,m\\
& h_i(x)=0,\quad j=1,...,r
\end{align}
$$

$D=dom(f)\cap \left\{\cap_{i=1}^m dom(g_i)\right\}\cap \left\{\cap_{j=1}^p dom(h_j)\right\}$ (common domain of all the functions)

### 2. convex optimization problem

if f and $g_i,i=1,...,m$ are convex, and $h_j, j=1,...,p$ are affine: 
$$
h_j(x)=a_j^Tx+b_j, j=1,...,p
$$

### 3. Why convexity?

![image-20201117223440651](2020-11-17-Convex-Optimization-1.assets/image-20201117223440651.png)

## 二次终止性

- 正定二次函数$f(x)=\frac{1}{2}x^TAx+b^Tx+c(A为正定矩阵)$存在唯一极小点
- 一般函数极小点附近可用正定二次函数近似
- 能否求出正定二次函数的极小点是检验算法标准之一
- **二次终止性**：对任意正定二次函数，从任意初始点出发，经过有限步迭代求出极小点

## 梯度方向是函数值增加最快的方向

目标：使损失函数最小，而梯度反方向是函数值减小最快的方向，所以沿梯度反方向更新参数。详见Reference 3.

实际的**非精确线搜索**中：**“不要太正交”**——只要选择的下降方向不要太接近梯度的正交方向，那么采用满足Wolfe准则的步长，算法就会最终收敛到函数极小点。

Reference

1. https://www.cnblogs.com/shine-lee/p/10950963.html
2. http://www.stat.cmu.edu/~ryantibs/convexopt/
3. https://zhuanlan.zhihu.com/p/38525412梯度的方向为什么是函数值增加最快的方向？