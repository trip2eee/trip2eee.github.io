---
layout: post
title: "MMSE Estimator"
categories: "Tracking"
tags: [KalmanFilter]
use_math: true
comments: true
---

# MMSE Estimator

## Minimum Mean-Squared Error (MMSE) Estimator
Minimum Mean-Squared Error (MMSE) estimator estimates $\hat{x}$ in such a way that mean squared-error is minimized.

$\hat{x} = arg min E\left[ \left(X - \hat{x}\right)^T \left(X - \hat{x}\right) \mid Z_k=z_k\right]$

$J=E\left[ \left(X - \hat{x}\right)^T \left(X - \hat{x}\right) \mid Z_k=z_k\right]$

$=E\left[X^TX - X^T\hat{x} - \hat{x}^TX + \hat{x}^T\hat{x}  \mid Z_k=z_k \right]$
$=E\left[X^T X\mid Z_k=z_k \right] - 2\hat{x}^TE\left[X\mid Z_k=z_k \right] + \hat{x}^T\hat{x}$

To find $\hat{x}$ such that minimizes $J$, differentiate $J$ with respect to $\hat{x}$.

$\frac{\partial J}{\partial \hat{x}} = -2E\left[X \mid Z_k=z_k\right] + 2\hat{x}$

$\hat{x} = E\left[X \mid Z_k=z_k\right]$



If $X$ and $Z$ are jointly Gaussian

$X \sim \mathcal N\left(\mu_X, P_{XX}\right)$

$Z \sim \mathcal N\left(\mu_Z, P_{ZZ}\right)$

$Y=\begin{bmatrix}X \\\\ Z\end{bmatrix} \sim \mathcal N\left(\mu_Y, P_{YY}\right)$

$p_{X \mid Z} = \frac{p_{XY}\left(x, z\right)}{p_Z\left(z\right)}=\frac{p_Y\left(y\right)}{p_Z\left(z\right)}$

$=\frac{\sqrt{\left(2\pi\right)^p det P_{ZZ}}}{\sqrt{\left(2\pi\right)^{n+p} det P_{YY}}}exp\left(-\frac{1}{2} \left( \left(y - \mu_Y\right)^TP_{YY}^{-1}\left(y - \mu_Y\right) - \left(z - \mu_Z\right)^TP_{ZZ}^{-1}\left(z - \mu_Z\right)\right) \right)$

By the Eq.8 and Eq.9 in [Gaussian random vector](https://trip2eee.github.io/tracking/2022/07/21/Gaussian-random-vector.html),

$p_{X \mid Z}(x \mid z) = \frac{1}{\sqrt{\left(2\pi\right)^n det P_{XX \mid Z}}} exp\left(-\frac{1}{2} \left(x - E\left[X \mid Z=z\right]\right)^T P_{XX \mid Z}^{-1} \left(x - E\left[X \mid Z=z\right]\right) \right)$

$E\left[X \mid Z=z \right] = \mu_X + P_{XZ}P_{ZZ}^{-1}(z-\mu_Z)$

$P_{XX \mid Z} = P_{XX} - P_{XZ}P_{ZZ}^{-1}P_{ZX}$


## Linear Measurement Model

If we let $Z=HX+V$, where measurement noise $V \sim \mathcal N\left(0, R\right)$

$\mu_Z = E\left[Z\right] = E\left[HX + V\right] = HE\left[X\right] = H\mu_X$

### Derivation of Measurement Covariance $P_{ZZ}$

$P_{ZZ} = E\left[\left(Z - \mu_Z\right)\left(Z - \mu_Z\right)^T\right]$

$= E\left[\left(H\left(X - \mu_X\right) + V\right) \left(H\left(X - \mu_X\right) + V\right)^T \right]$

$= HP_{XX}H^T + E\left[H\left(X-\mu_X\right)V^T\right] + E\left[V\left(X-\mu_X\right)^TH^T\right] + R$

$= HP_{XX}H^T + R$


### Derivation of Covariance between X and Z $P_{XZ}$

$P_{XZ} = E\left[\left(X - \mu_X \right)\left(Z-\mu_Z\right)^T\right]$

$=E\left[\left(X - \mu_X \right)\left(H\left(X-\mu_X\right)+V\right)^T\right]$

$=P_{XX}H^T + E\left[\left(X - \mu_X \right)V^T\right]$

$=P_{XX}H^T$


### The result of MMSE estimator

$\hat{x} = \mu_X + P_{XX}H^T \left( HP_{XX}H^T + R\right)^{-1} \left(z - H\mu_X \right)$

$P_{XX\mid Z} = P_{XX} - P_{XX}H^T\left(HP_{XX}H^T + R\right)^{-1}HP_{XX}$

## Comparison to measurement update of Kalman filter

$K = P_{XX}H^T\left(HP_{XX}H^T + R\right)^{-1}$

$\hat{x} = \mu_X + K\left(z - H\mu_X\right)$

$P_{XX \mid Z} = \left(I - KH\right)P_{XX}$


# Reference
[1] 박성수, 수학으로 풀어보는 칼만 필터 알고리즘, 위키북스(2020), p113-127.

