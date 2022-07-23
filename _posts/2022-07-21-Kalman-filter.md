---
layout: post
title: "Derivation of Kalman filter"
categories: "Tracking"
tags: [KalmanFilter]
use_math: true
comments: true
---

# Derivation of Kalman filter

## Assumption
* Process noise $w \sim \mathcal{N}\left(0, Q\right)$
* Measurement noise $v \sim \mathcal{N}\left(0, R\right)$
* $w$ and $v$ are independent.

## Bayes filter
State space equation

\begin{align} x(k+1) = f(x(k), u(k), w(k), k) \end{align}

Measurement model 

\begin{align} z(k) = h(x(k), v(k), k) \end{align}

Markov assumption

\begin{align} p(x(k) \mid x(k-1), x(k-2), ..., x(0), Z_{k-1}, U_{k-1}) = p(x(k) \mid x(k-1), u(k-1)) \label{eq_system_model} \end{align}

\begin{align} p(z(k) \mid x(k), Z_{k-1}, U_{k-1}) = p(z(k) \mid x(k)) \label{eq_meas_model} \end{align}


Eq.$\ref{eq_system_model}$ is the pdf of state transition based on the previous state and the previous input. Eq.$\ref{eq_meas_model}$ is the pdf of measurements for the current state.


Bayes filter estimates conditional probability $p(x(k) \mid Z_k, U_{k-1})$ using Eq.$\ref{eq_system_model}$ and Eq.$\ref{eq_meas_model}$.

\begin{align} p(x(k) \mid Z_k, U_{k-1}) = \frac{p(Z_k \mid x(k), U_{k-1}) p(x(k) \mid U_{k-1})}{p(Z_k \mid U_{k-1})} \end{align}

\begin{align} =\frac{p(z(k), Z_{k-1} \mid x(k), U_{k-1}) p(x(k) \mid U_{k-1})}{p(z(k) \mid Z_{k-1}, U_{k-1})} \end{align}

\begin{align} =\frac{p(z(k) \mid Z_{k-1}, x(k), U_{k-1}) p(Z_{k-1} \mid x(k), U_{k-1}) p(x(k) \mid U_{k-1})}{p(z(k) \mid Z_{k-1}, U_{k-1}) p(Z_{k-1} \mid U_{k-1})} \label{eq_interim1} \end{align}

$p(Z_{k-1} \mid x(k), U_{k-1})$ in Eq.$\ref{eq_interim1}$ can be computed as

\begin{align} p(Z_{k-1} \mid x(k), U_{k-1}) = \frac{ p(x(k) \mid Z_{k-1}, U_{k-1}) p(Z_{k-1} \mid U_{k-1}) } {p(x(k) \mid U_{k-1})} \label{eq_interim2} \end{align}

If we replace $p(Z_{k-1} \mid x(k), U_{k-1})$ in Eq.$\ref{eq_interim1}$ with Eq.$\ref{eq_interim2}$,

\begin{align} p(x(k) \mid Z_k, U_{k-1}) = \frac{ p(z(k) \mid Z_{k-1}, x(k), U_{k-1}) p(x(k) \mid U_{k-1}) \cdot p(Z_{k-1} \mid x(k), U_{k-1})}{ p(z(k) \mid Z_{k-1}, U_{k-1}) p(Z_{k-1} \mid U_{k-1}) } \end{align}

\begin{align} = \frac{ p(z(k) \mid Z_{k-1}, x(k), U_{k-1}) p(x(k) \mid U_{k-1}) \cdot p(x(k) \mid Z_{k-1}, U_{k-1}) p(Z_{k-1} \mid U_{k-1}) }{ p(z(k) \mid Z_{k-1}, U_{k-1}) p(Z_{k-1} \mid U_{k-1}) \cdot p(x(k) \mid U_{k-1})} 
\end{align}

\begin{align} = \frac{ p(z(k) \mid x(k), Z_{k-1}, U_{k-1}) \cdot p(x(k) \mid Z_{k-1}, U_{k-1}) }{ p(z(k) \mid Z_{k-1}, U_{k-1})} \label{eq_interim3} \end{align}

By applying measurement model Eq.$\ref{eq_meas_model}$, Eq.$\ref{eq_interim3}$ becomes

\begin{align} p(x(k) \mid Z_k, U_{k-1}) = \frac{ p(z(k) \mid x(k)) p(x(k) \mid Z_{k-1}, U_{k-1}) } {p(z(k) \mid Z_{k-1}, U_{k-1})} \label{eq_interim4} \end{align}

Description of pdfs in Eq.$\ref{eq_interim4}$ are as follows: 

* $p(x(k) \mid Z_{k-1}, U_{k-1})$ a priori pdf because it's obtained before measuring $z(k)$.
* $p(x(k) \mid Z_k, U_{k-1})$ : a posteriori pdf because it's obtained after measuring $z(k)$.
* $p(z(k) \mid x(k))$ : likelihood function.
* $p(x(k) \mid Z_{k-1}, U_{k-1})$ : Normalizing function defined as follows

\begin{align} p(x(k) \mid Z_{k-1}, U_{k-1}) = \int_{x(k)} {p(z(k) \mid x(k)) p(x(k) \mid Z_{k-1}, U_{k-1}) dx(k)} \label{eq_norm_func}\end{align}

If we apply Eq.$\ref{eq_norm_func}$ to Eq.$\ref{eq_interim4}$, 

\begin{align} p(x(k) \mid Z_k, U_{k-1}) = \frac{ p(z(k) \mid x(k)) p(x(k) \mid Z_{k-1}, U_{k-1}) }{ \int_{x(k)} {p(z(k) \mid x(k)) p(x(k) \mid Z_{k-1}, U_{k-1}) dx(k)} } \label{eq_meas_update} \end{align}

Eq.$\ref{eq_meas_update}$ is measurement update.

If we expand $p(x(k) \mid Z_{k-1}, U_{k-1})$ in Eq.$\ref{eq_meas_update}$, 

\begin{align} p(x(k) \mid Z_{k-1}, U_{k-1}) = \int_{x(k-1)} p(x(k) \mid x(k-1), Z_{k-1}, U_{k-1}) p(x(k-1) \mid Z_{k-1}, U_{k-1}) dx(k-1) \end{align}

\begin{align} = \int_{x(k-1)} p(x(k) \mid x(k-1), u(k-1)) p(x(k-1) \mid Z_{k-1}, U_{k-2}) dx(k-1) \label{eq_time_update} \end{align}

Eq.$\ref{eq_time_update}$ is time update (prediction).

## Kalman filter model

\begin{align} x(k+1) = F(k)x(k) + G(k)u(k) + G_w(k)w(k) \label{eq_kf_pred_model1}\end{align}

\begin{align} z(k) = H(k)x(k) + v(k) \label{eq_kf_meas_model1}\end{align}

Let's compute the mean of $x(k+1)$

\begin{align} E\left[ x(k+1) \right] = E\left[ F(k)x(k) + G(k)u(k) + G_w(k)w(k) \right] \end{align}

\begin{align} = F(k)E\left[ x(k) \right] + G(k)u(k) + G_w(k)E\left[ w(k) \right] \end{align}

\begin{align} = F(k)E\left[ x(k) \right] + G(k)u(k) \label{eq_kf_pred_model2}\end{align}

The mean value of measurement vector is compuated as

\begin{align} E\left[ z(k) \right] = E\left[ H(k)x(k) + v(k) \right] \end{align}

\begin{align} = H(k) E\left[ x(k) \right] + E\left[ v(k) \right] \end{align}

\begin{align} = H(k) E\left[ x(k) \right] \label{eq_kf_meas} \end{align}

Let state error $\tilde{x}(k) = x(k) - E\left[ x(k) \right] $. Then error propagation is obtained by Eq.$\ref{eq_kf_pred_model1}$, Eq.$\ref{eq_kf_meas_model1}$ and Eq.$\ref{eq_kf_pred_model2}$ as follows

\begin{align} \tilde{x}(k + 1) = F(x)\tilde{x}(k) + G_w(k)w(k) \label{ep_kf_error_prop}\end{align}

From Eq.$\ref{ep_kf_error_prop}$ error covariance becomes

\begin{align} P(k+1) = E\left[ \tilde{x}(k+1) \tilde{x}^T(k+1) \right] \end{align}

\begin{align} = E\left[ \left( F(k)\tilde{x}(k) +G_w(k)w(k) \right) \left( F(k)\tilde{x}(k) +G_w(k)w(k) \right)^T \right] \end{align}

\begin{align} = F(k)P(k)F^T(k) + G_w(k)Q(k)G^T_w(k) \end{align}

Let meazurement error $\tilde{z} = z(k) - E\left[ z(k) \right]$. Then from Eq.$\ref{eq_kf_meas_model1}$, Eq.$\ref{eq_kf_meas}$ the error covariance of measurement vector becoms

\begin{align} P_{zz}(k) = E\left[ \tilde{z}(k) \tilde{z}^T(k) \right] \end{align}

\begin{align} = H(k) E\left[ \tilde{x}(k) \tilde{x}^T(k) \right] H^T(k) + E\left[ v(k) v^T(k) \right] + H(k)E\left[ \tilde{x}(k) v^T(k)\right] + E\left[ v(k)\tilde{x}^T(k)\right]H^T(k) \end{align}

\begin{align} = H(k) P(k) H^T(k) + R(k) \label{eq_kf_pzz} \end{align}

Covariance between $x(k)$ and $z(k)$ is as follows

\begin{align} P_{xz}(k) = E\left[ \tilde{x}(k) \tilde{z}^T(k) \right] = E\left[ \tilde{x}(k) \left(H(k) \tilde{x}(k) + v(k)\right)^T \right] \end{align}

\begin{align} = E\left[ \tilde{x}(k)\tilde{x}^T(k) \right] H^T(k) + E\left[ \tilde{x}(k) v^T(k) \right] = P(k)H^T(k) \label{eq_kf_pxz} \end{align}

\begin{align} \begin{bmatrix} x(k) \\\\ z(k) \end{bmatrix} \sim N \left( \begin{bmatrix} \bar{x}(k) \\\\ \bar{z}(k) \end{bmatrix}, \begin{bmatrix}P(k) & P_{xz}(k) \\\\ P^T_{xz}(k) & P_{zz}(k) \end{bmatrix} \right)\end{align}

where $\bar{x}(k) = E \left[ x(k) \right]$ and $\bar{z}(k) = E \left[ z(k) \right]$.

## Derivation of Kalman filter
$x(k)$ and $z(k)$ are jointly Gaussian. Therefore,

\begin{align} p(x(k) \mid Z_k) = N\left(x(k) \mid \hat{x}(k \mid k), P(k \mid k)\right) \end{align}

\begin{align} p(x(k) \mid Z_{k-1}) = N\left(x(k) \mid \hat{x}(k \mid {k-1}), P(k \mid {k-1})\right) \end{align}

where

$\hat{x}(k \mid k) = E\left[x(k) \mid Z_k \right]$

$P(k \mid k) = E\left[\left(x(k) - \hat{x}(k \mid k)\right) \left(x(k) - \hat{x}(k \mid k)\right) \mid Z_k\right]$

$\hat{x}(k \mid k-1) = E\left[x(k) \mid Z_{k-1} \right]$

$P(k \mid k-1) = E\left[\left(x(k) - \hat{x}(k \mid k-1)\right) \left(x(k) - \hat{x}(k \mid k-1)\right) \mid Z_{k-1}\right]$


\begin{align} p(x(k), z(k) \mid Z_{k-1}) = N\left( \begin{bmatrix}x(k) \\\\ z(k)\end{bmatrix} \mid \begin{bmatrix} \hat{x}(k \mid k-1) \\\\ \hat{z}(k \mid k-1)\end{bmatrix}, \begin{bmatrix} P(k \mid k-1) & P_{xz}(k \mid k-1) \\\\ P^T_{xz}(k \mid k-1) & P_{zz}(k \mid k-1) \end{bmatrix}  \right)\end{align}

By using Eq.$\ref{eq_kf_meas}$ measurement prediction $\hat{z}(k \mid k-1)$ can be computed as follows
\begin{align} \hat{z}(k \mid k-1) = E\left[z(k) \mid Z_{k-1}\right] = E\left[H(k)x(k) + v(k) \mid Z_{k-1} \right] = H(k) \hat x(k \mid {k-1})\end{align}

Let measurement residual (innovation) $\tilde{z}(k \mid k-1) = z(k) - \hat{z}(k \mid k-1)$. Then from Eq.$\ref{eq_kf_pzz}$, measurement error covariance $P_{zz}(k \mid k-1)$ becomes

\begin{align} P_{zz}(k \mid k-1) = E\left[ \tilde{z}(k \mid k-1) \tilde{z}^T(k \mid k-1) \mid Z_{k-1} \right] = H(k)P(k \mid k-1)H^T(k) + R(k) \end{align}

If we define prediction error $\tilde{x}(k \mid k - 1) = x(k) - \hat{x}(k \mid k - 1)$, $P_{xz}(k \mid k-1)$ becomes as follows Eq.$\ref{eq_kf_pxz}$

\begin{align} P_{xz}(k \mid k-1) = E\left[ \tilde{x}(k \mid k-1) \tilde{z}^T(k \mid k-1) \mid Z_{k-1} \right] = P(k \mid k-1)H^T(k) \end{align}

From Eq.$\ref{eq_interim4}$, 

\begin{align} p(x(k) \mid Z_k) = p(x(k) \mid z(k), Z_{k-1}) = N\left(x(k) \mid \hat{x}(k \mid k), P(k \mid k) \right) \end{align}


### Measurement Update

By the Eq.8 and Eq.9 in [Gaussian random vector](Gaussian-random-vector.html), the expectations of the following pdfs are obtained.

\begin{align} \hat{x}(k \mid k) \equiv E\left[ x(k) \mid z(k), Z_{k-1}\right] = E\left[ x(k) \mid Z_k \right] \end{align}

\begin{align} = E\left[ x(k) \mid Z_{k-1} \right] + K(k)(z(k) - E\left[ z(k) \mid Z_{k-1} \right] \end{align}

\begin{align} = \hat{x}(k \mid k-1) + K(k)\left(z(k) - H(k)\hat{x}(k \mid k-1)\right) \end{align}

\begin{align} P(k \mid k) = E\left[ \tilde{x}(k \mid k-1) \tilde{x}^T(k \mid k-1) \mid Z_{k-1} \right] - P_{xz}(k \mid k-1) P_{zz}^{-1} (k \mid k-1)P^T_{xz}(k \mid k-1)\end{align}

\begin{align} = P(k \mid k-1) - P_{xz}(k \mid k-1) P_{zz}^{-1} (k \mid k-1) P_{xz}^T(k \mid k-1) \end{align}
\begin{align} = \left(I - K(k)H(k)\right)P(k \mid k-1) \end{align}


where Kalman gain $K(k)$ is as follows

\begin{align} K(k) = P_{xz}(k \mid k - 1) P^{-1}_{zz}(k \mid k-1) \end{align}
\begin{align} = P(k \mid k-1)H^T(k) \left( H(k)P(k \mid k-1)H^T(k) + R(k)\right)^{-1} \end{align}

### Time Update
\begin{align} p(x(k+1) \mid Z_k) = N(x(k+1) \mid \hat{x}(k+1 \mid k), P(k+1 \mid k)) \end{align}

\begin{align} \hat{x}(k + 1 \mid k) = E\left[ x(k+1) \mid Z_k \right] = E\left[ F(k)x(k) + G(k)u(k) + G_w(k)w(k) \mid Z_k \right] \end{align}

\begin{align} = F(k)\hat{x}(k\mid k) + G(k)u(k) \end{align}


\begin{align} P(k + 1 \mid k) = E\left[ \left(x(k+1) - \hat{x}(k+1 \mid k)\right)\left(x(k+1) - \hat{x}(k+1 \mid k)\right)^T \mid Z_k \right] \end{align}

\begin{align} = F(k)P(k)F^T(k) + G_w(k)Q(k)G^T_w(k) \end{align}

# Reference
[1] 박성수, 수학으로 풀어보는 칼만 필터 알고리즘, 위키북스(2020), p113-127.



