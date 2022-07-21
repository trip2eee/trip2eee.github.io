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

\begin{align} x(k+1) = f(x(k), u(k), w(k), k) \end{align}

Measurement model 

\begin{align} z(k) = h(x(k), v(k), k) \end{align}

Markov assumption

\begin{align} p(x(k) \mid x(k-1), x(k-2), ..., x(0), Z_{k-1}, U_{k-1}) = p(x(k) \mid x(k-1), u(k-1)) \label{markov_assumption1} \end{align}

\begin{align} p(z(k) \mid x(k), Z_{k-1}, U_{k-1}) = p(z(k) \mid x(k)) \label{markov_assumption2}  \end{align}

Bayes filter estimates conditional probability $p(x(k) \mid Z_k, U_{k-1})$ using equation $\ref{markov_assumption1}$ and $\ref{markov_assumption2}$.

\begin{align} p(x(k) \mid Z_k, U_{k-1}) = \frac{p(Z_k \mid x(k), U_{k-1}) p(x(k) \mid U_{k-1})}{p(Z_k \mid U_{k-1})} \end{align}



# Reference
[1] 박성수, 수학으로 풀어보는 칼만 필터 알고리즘, 위키북스(2020), p113-127.

