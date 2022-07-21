---
layout: post
title: "Derivation of Kalman filter"
categories: "Tracking"
tags: [KalmanFilter]
use_math: true
comments: true
---

# Derivation of Kalman filter
### Assumption
* Process noise $w \sim \mathcal{N}\left(0, Q\right)$
* Measurement noise $v \sim \mathcal{N}\left(0, R\right)$
* $w$ and $v$ are independent.

## Bayes filter
State space equation

$$x(k+1) = f(x(k), u(k), w(k), k)$$

Measurement model 

$$\begin{equation*}z(k) = h(x(k), v(k), k)\end{equation*}$$

Markov assumption

$$\begin{align} p(x(k) | x(k-1), x(k-2), ..., x(0), Z_{k-1}, U_{k-1}) = p(x(k) | x(k-1), u(k-1)) \end{align}$$

$$\begin{align} p(z(k)|x(k), Z_{k-1}, U_{k-1}) = p(z(k) | x(k)) \end{align}$$

Bayes filter estimates conditional probability $p(x(k)|Z_k, U_{k-1})$ using equation 3 and 4.

$$\begin{align} p(x(k)|Z_k, U_{k-1}) = \frac{p(Z_k|x(k), U_{k-1}) p(x(k)|U_{k-1})}{p(Z_k|U_{k-1})} \end{align}$$



# Reference
[1] 박성수, 수학으로 풀어보는 칼만 필터 알고리즘, 위키북스(2020), p113-127.

