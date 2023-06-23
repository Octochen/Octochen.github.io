---
title: 最小二乘估计和Kalman滤波
date: 2023-03-07 22:31:43
mathjax: true
---

> ##### 最小二乘估计和加权最小二乘估计
> - 最小二乘估计
>   - 考虑噪声扰动下的量测方程：$y(k) = h(k)x + v(k)$
>     - 量测扩维：$y_{1:k}=H_{1:k}x+v_{1:k}$
>     - 假设$v_{1:k}$是零均值协方差为$\sigma^2I$的高斯白噪声（白噪声就是时间不相关的噪声，功率谱密度函数为0） 
>   - 最小二乘估计：$\hat x = \arg \min_{x} \|y_{1:k}-H_{1:k}x\|_2^2$
>     - $\hat{x} = \left( H^{T}_{1:k}H_{1:k} \right)^{- 1}H^{T}_{1:k}y_{1:k}$（这里开始==假设$H_{1:k}$是列满秩==的，而没有假设方程组无解，便于后面的说明）
>       - 假设$H_{1:k}$行满秩，则得到最小范数估计
>     - 最小二乘估计只保证量测与量测估计值的误差平方和最小，不需要$v_{1:k}$的任何统计信息
>     - 性质：无偏性，即$\mathrm E(x-\hat x)=0$
>     - 性质：==最小方差（协方差更恰当）==无偏==线性==估计。
>       - 考虑线性估计器：$\tilde x=My_{1:k}$，满足无偏性$\mathrm E(x-\tilde x)=\mathrm E [(I-MH_{1:k})x-Mv_{1:k}]=0$，即$I-MH_{1:k}=0$。
>       - 无偏线性估计的方差=误差协方差：$V(\tilde x)=\mathrm E[(\hat x-\mathrm E\hat x)(\hat x-\mathrm E\hat x)^T]=\mathrm E[(\hat x-x)(\hat x-x)^T]=P(\tilde x)=MM^T$
>       - 最小二乘估计的方差：$P(\hat x)=(H^T_{1:k} H_{1:k})^{-1}$
>       - 有矩阵不等式$M[I-H_{1:k}(H^T_{1:k} H_{1:k})^{-1}H^T_{1:k}]M^T \ge 0$，其中$H_{1:k}(H^T_{1:k} H_{1:k})^{-1}H^T_{1:k}$为正交投影矩阵
>       - 也可以极小化估计方差的迹$J=\mathrm {tr}\{\mathrm E[(x-\hat x)(x-\hat x)^T]\}$得到线性无偏最小方差估计，发现恰恰是最小二乘估计。
> - 加权最小二乘估计
>   - 假设零均值高斯白噪声$v_{1:k}$的协方差矩阵为$\Sigma$
>   - 加权最小二乘估计：$\hat x=\arg \min_x \|y_{1:k} - H_{1:k}x \|_{W}^2$
>     - $\hat{x} = \left( H^{T}_{1:k}WH_{1:k} \right)^{- 1}H^{T}_{1:k}Wy_{1:k}$（这里==假设$H^{T}_{1:k}WH_{1:k}$是非奇异的==，便于后面的说明）
>     - $P=\left( H^{T}_{1:k}WH_{1:k} \right)^{- 1}H^{T}_{1:k}W \Sigma WH_{1:k} \left( H^{T}_{1:k}WH_{1:k} \right)^{- 1}$
>   - 权重矩阵$W$的选择：当$W=\Sigma^{-1}$时，加权最小二乘估计的误差协方差最小（凑矩阵施瓦兹不等式法^[《2009_Kalman Filtering with Real-Time Applications》第一章]）。
>     - $\hat x=\left( H^{T}_{1:k} \Sigma^{-1} H_{1:k} \right)^{- 1}H^{T}_{1:k} \Sigma^{-1} y_{1:k}$
>     - $P=\left(H^T_{1:k} \Sigma^{-1} H_{1:k}\right)^{-1}$
>   - 此时，加权最小二乘估计恰恰是线性无偏最小方差估计
>     - 考虑无偏线性估计$\hat x=Ky_{1:k}$，满足无偏性$KH_{1:k}=I$
>     - 极小化估计误差协方差的迹$J=\mathrm {tr}\{\mathrm E[(x-\hat x)(x-\hat x)^T]\}$
>     - 得到最优线性增益恰恰为$K=\left( H^{T}_{1:k} \Sigma^{-1} H_{1:k} \right)^{- 1}H^{T}_{1:k} \Sigma^{-1}$
> - 递归最小二乘
>   - 由$P(k)=\left(H^T_{1:k} \Sigma^{-1} H_{1:k}\right)^{-1}$得到$P(k)$和$P(k-1)$的关系
>     - $P(k)=\left( H^{T}_{1:k-1}H_{1:k-1} + h^T(k)h(k) \right)^{- 1}$
>     - 由矩阵逆引理可知$P(k)=P(k-1)-P(k-1)h^T(k)\left(I+h(k)P(k-1)h^T(k)\right)^{-1}h(k)P(k-1)$
>   - 由$\hat x(k)=\left( H^{T}_{1:k}H_{1:k} \right)^{- 1}H^{T}_{1:k}y_{1:k}$直接得到$\hat x(k)$和$\hat x(k-1)$的关系
>     - $\hat x(k)=\left( H^{T}_{1:k-1}H_{1:k-1} + h^T(k)h(k) \right)^{- 1} \left(H^{T}_{1:k-1}y_{1:k-1}+h^T(k)y(k)\right)$
>     - 得到$\hat x(k)=\hat x(k-1) + P(k)h^T(k)(y(k)-h(k)\hat x(k-1))$。
>     - ==细节==：$P(k-1)h^T(k)\left(I+h(k)P(k-1)h^T(k)\right)^{-1}h(k)=P(k)h^T(k)$