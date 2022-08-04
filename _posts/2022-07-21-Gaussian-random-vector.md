---
layout: post
title: "Gaussian random vector"
categories: "Tracking"
tags: [KalmanFilter]
use_math: true
comments: true
---

# Gaussian random vector

## Mean and Variance of Gaussian random vector

Let $X \sim \mathcal{N}\left(\mu_x, P_{xx}\right)$ and $Z \sim \mathcal{N}\left(\mu_z, P_{zz}\right)$ are jointly normally distributed.

\begin{align} Y = \begin{bmatrix} X \\\\ Z \end{bmatrix} \end{align}

\begin{align} P_{YY} = \begin{bmatrix} P_{XX} & P_{XZ} \\\\ P_{ZX} & P_{ZZ} \end{bmatrix} \label{eq_pyy}\end{align}


Then the conditional pdf of $X$ can be given as follows

\begin{align} p_{X \mid Z} (x \mid z) = \frac{p_{XZ}(x,z)}{p_Z(z)} = \frac{p_Y(y)}{p_Z(z)} \end{align}

\begin{align} = \frac{p_{XZ}(x,z)}{p_Z(z)} = \frac{p_Y(y)}{p_Z(z)} \end{align}

\begin{align} = \frac{\sqrt{(2\pi)^p detP_{ZZ}}}{\sqrt{(2\pi)^{n+p}det P_{YY}}} exp\left( -\frac{1}{2} \left\\{  (y-\mu_Y)^T P_{YY}^{-1} (y-\mu_Y) - (z-\mu_Z)^T P_{ZZ}^{-1} (z-\mu_Z) \right\\} \right) \label{eq_pxz}\end{align}

where $n$ and $p$ are dimensions of $X$ and $Z$, respectively.

Then the inverse of Eq.$\ref{eq_pyy}$ can be computed by Schur complement [1].

\begin{align} P_{YY}^{-1} = \left( \begin{bmatrix} I & P_{XZ}P_{ZZ}^{-1} \\\\ 0 & I \end{bmatrix} \begin{bmatrix} P_{XX}-P_{XZ}P_{ZZ}^{-1}P_{ZX} & 0 \\\\ 0 & P_{ZZ} \end{bmatrix} \begin{bmatrix} I & 0 \\\\ P_{ZZ}^{-1}P_{ZX} & I \end{bmatrix}\right)^{-1}\end{align}

\begin{align} = \begin{bmatrix} I & 0 \\\\ -P_{ZZ}^{-1}P_{ZX} & I \end{bmatrix} \begin{bmatrix} \left(P_{XX}-P_{XZ}P_{ZZ}^{-1}P_{ZX}\right)^{-1} & 0 \\\\ 0 & P_{ZZ}^{-1} \end{bmatrix} \begin{bmatrix} I & -P_{XZ}P_{ZZ}^{-1} \\\\ 0 & I \end{bmatrix}\end{align}

\begin{align} = \begin{bmatrix} D^{-1} & -D^{-1} P_{XZ} P_{ZZ}^{-1} \\\\ -P_{ZZ}^{-1}P_{ZX}D^{-1} & P_{ZZ}^{-1}+P_{ZZ}^{-1}P_{ZX}D^{-1}P_{XZ}P_{ZZ}^{-1} \end{bmatrix} \end{align}

where $D = P_{XX} - P_{XZ}P_{ZZ}^{-1}P_{ZX}$

The equation in $\\{ \cdot \\}$ of Eq.$\ref{eq_pxz}$ can be simplified.

$ (y - \mu_Y)^T P_{YY}^{-1} (y - \mu_Y) - (z - \mu_Z)^T P_{ZZ}^{-1} (z - \mu_Z) $

$ = (x - \mu_X)^T D^{-1} (x - \mu_X) - (x - \mu_X)^T D^{-1}P_{XZ}P_{ZZ}^{-1} (z - \mu_Z) - (z - \mu_Z)^T P_{ZZ}^{-1}P_{ZX}D^{-1}(x - \mu_X) $

$ + (z-\mu_Z)^T\left(P_{ZZ}^{-1} + P_{ZZ}^{-1}P_{ZX}D^{-1}P_{XZ}P_{ZZ}^{-1}\right)(z-\mu_Z) - (z - \mu_Z)^T P_{ZZ}^{-1} (z - \mu_Z) $

Cancel $(z - \mu_Z)^T P_{ZZ}^{-1} (z - \mu_Z)$ out.

$ = (x - \mu_X)^T D^{-1} (x - \mu_X) - (x - \mu_X)^T D^{-1}P_{XZ}P_{ZZ}^{-1} (z - \mu_Z) - (z - \mu_Z)^T P_{ZZ}^{-1}P_{ZX}D^{-1}(x - \mu_X) $

$ + (z-\mu_Z)^T\left(P_{ZZ}^{-1}P_{ZX}D^{-1}P_{XZ}P_{ZZ}^{-1}\right)(z-\mu_Z) $

$ = \left[(x - \mu_X) - P_{XZ}P_{ZZ}^{-1}(z-\mu_Z) \right]^T D^{-1} \left[(x - \mu_X) - P_{XZ}P_{ZZ}^{-1}(z-\mu_Z) \right] $

$ = \left[x - (\mu_X + P_{XZ}P_{ZZ}^{-1}(z-\mu_Z)) \right]^T D^{-1} \left[(x - (\mu_X + P_{XZ}P_{ZZ}^{-1}(z-\mu_Z)) \right] $

$ = \left[x - \mu_{X \mid Z} \right]^T P_{X \mid Z}^{-1} \left[(x - \mu_{X \mid Z} \right] $

Therefore

\begin{align} \mu_{X \mid Z} = \mu_X + P_{XZ}P_{ZZ}^{-1}(z-\mu_Z) \end{align}

\begin{align} P_{X \mid Z} = D = P_{XX} - P_{XZ}P_{ZZ}^{-1}P_{ZX} \end{align}

# Reference
[1] https://en.wikipedia.org/wiki/Schur_complement