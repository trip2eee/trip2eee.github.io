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


$\ref{eq_system_model}$ is the pdf of state transition based on the previous state and the previous input. $\ref{eq_meas_model}$ is the pdf of measurements for the current state.


Bayes filter estimates conditional probability $p(x(k) \mid Z_k, U_{k-1})$ using equation $\ref{eq_system_model}$ and $\ref{eq_meas_model}$.

\begin{align} p(x(k) \mid Z_k, U_{k-1}) = \frac{p(Z_k \mid x(k), U_{k-1}) p(x(k) \mid U_{k-1})}{p(Z_k \mid U_{k-1})} \end{align}

\begin{align} =\frac{p(z(k), Z_{k-1} \mid x(k), U_{k-1}) p(x(k) \mid U_{k-1})}{p(z(k) \mid Z_{k-1}, U_{k-1})} \end{align}

\begin{align} =\frac{p(z(k) \mid Z_{k-1}, x(k), U_{k-1}) p(Z_{k-1} \mid x(k), U_{k-1}) p(x(k) \mid U_{k-1})}{p(z(k) \mid Z_{k-1}, U_{k-1}) p(Z_{k-1} \mid U_{k-1})} \label{eq_interim1} \end{align}

$p(Z_{k-1} \mid x(k), U_{k-1})$ in $\ref{eq_interim1}$ can be computed as

\begin{align} p(Z_{k-1} \mid x(k), U_{k-1}) = \frac{ p(x(k) \mid Z_{k-1}, U_{k-1}) p(Z_{k-1} \mid U_{k-1}) } {p(x(k) \mid U_{k-1})} \label{eq_interim2} \end{align}

If we replace $p(Z_{k-1} \mid x(k), U_{k-1})$ in $\ref{eq_interim1}$ with $\ref{eq_interim2}$,

\begin{align} p(x(k) \mid Z_k, U_{k-1}) = \frac{ p(z(k) \mid Z_{k-1}, x(k), U_{k-1}) p(x(k) \mid U_{k-1}) \cdot p(Z_{k-1} \mid x(k), U_{k-1})}{ p(z(k) \mid Z_{k-1}, U_{k-1}) p(Z_{k-1} \mid U_{k-1}) } \end{align}

\begin{align} = \frac{ p(z(k) \mid Z_{k-1}, x(k), U_{k-1}) p(x(k) \mid U_{k-1}) \cdot p(x(k) \mid Z_{k-1}, U_{k-1}) p(Z_{k-1} \mid U_{k-1}) }{ p(z(k) \mid Z_{k-1}, U_{k-1}) p(Z_{k-1} \mid U_{k-1}) \cdot p(x(k) \mid U_{k-1})} 
\end{align}

\begin{align} = \frac{ p(z(k) \mid x(k), Z_{k-1}, U_{k-1}) \cdot p(x(k) \mid Z_{k-1}, U_{k-1}) }{ p(z(k) \mid Z_{k-1}, U_{k-1})} \label{eq_interim3} \end{align}

By applying measurement model $\ref{eq_meas_model}$, $\ref{eq_interim3}$ becomes

\begin{align} p(x(k) \mid Z_k, U_{k-1}) = \frac{ p(z(k) \mid x(k)) p(x(k) \mid Z_{k-1}, U_{k-1}) } {p(z(k) \mid Z_{k-1}, U_{k-1})} \label{eq_interim4} \end{align}

Description of pdfs in $\ref{eq_interim4}$ are as follows: 

* $p(x(k) \mid Z_{k-1}, U_{k-1})$ a priori pdf because it's obtained before measuring $z(k)$.
* $p(x(k) \mid Z_k, U_{k-1})$ : a posteriori pdf because it's obtained after measuring $z(k)$.
* $p(z(k) \mid x(k))$ : likelihood function.
* $p(x(k) \mid Z_{k-1}, U_{k-1})$ : Normalizing function defined as follows

\begin{align} p(x(k) \mid Z_{k-1}, U_{k-1}) = \int_{x(k)} {p(z(k) \mid x(k)) p(x(k) \mid Z_{k-1}, U_{k-1}) dx(k)} \label{eq_norm_func}\end{align}

If we apply $\ref{eq_norm_func}$ to $\ref{eq_interim4}$, 

\begin{align} p(x(k) \mid Z_k, U_{k-1}) = \frac{ p(z(k) \mid x(k)) p(x(k) \mid Z_{k-1}, U_{k-1}) }{ \int_{x(k)} {p(z(k) \mid x(k)) p(x(k) \mid Z_{k-1}, U_{k-1}) dx(k)} } \label{eq_meas_update} \end{align}

$\ref{eq_meas_update}$ is measurement update.

If we expand $p(x(k) \mid Z_{k-1}, U_{k-1})$ in $\ref{eq_meas_update}$, 

\begin{align} p(x(k) \mid Z_{k-1}, U_{k-1}) = \int_{x(k-1)} p(x(k) \mid x(k-1), Z_{k-1}, U_{k-1}) p(x(k-1) \mid Z_{k-1}, U_{k-1}) dx(k-1) \end{align}

\begin{align} = \int_{x(k-1)} p(x(k) \mid x(k-1), u(k-1)) p(x(k-1) \mid Z_{k-1}, U_{k-2}) dx(k-1) \label{eq_time_update} \end{align}

$\ref{eq_time_update}$ is time update (prediction).


# Reference
[1] 박성수, 수학으로 풀어보는 칼만 필터 알고리즘, 위키북스(2020), p113-127.

