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

\begin{align} = \frac{\sqrt{(2\pi)^p detP_{ZZ}}}{\sqrt{(2\pi)^{n+p}det P_{YY}}} exp\left( -\frac{1}{2} \left\\{  (y-\mu_y)^T P_{YY}^{-1} (y-\mu_y) - (z-\mu_z)^T P_{ZZ}^{-1} (z-\mu_z) \right\\} \right) \label{eq_pxz}\end{align}

where $n$ and $p$ are dimensions of $X$ and $Z$, respectively.

Then the inverse of Eq.$\ref{eq_pyy}$ can also be expressed in the matrix form.

\begin{align} P_{YY}^{-1} = \begin{bmatrix} D^{-1} & -D^{-1} P_{XZ} P_{ZZ}^{-1} \\\\ -P_{ZZ}^{-1}P_{ZX}D^{-1} & P_{ZZ}^{-1}+P_{ZZ}^{-1}P_{ZX}D^{-1}P_{XZ}P_{ZZ}^{-1} \end{bmatrix} \end{align}

where

\begin{align}D = P_{XX} - P_{XZ}P_{ZZ}^{-1}P_{ZX} \end{align}

The equation in $\\{ \cdot \\}$ of Eq.$\ref{eq_pxz}$ can be simplified.

$ (y - \mu_y)^T P_{yy}^{-1} (y - \mu_y) - (z - \mu_z)^T P_{zz}^{-1} (z - \mu_z) $

$ = (x - \mu_x)^T D^{-1} (x - \mu_x) - (x - \mu_x)^T D^{-1}P_{xz}P_{zz}^{-1} (z - \mu_z) - (z - \mu_z)^T P_{zz}^{-1}P_{zx}D^{-1}(x - \mu_x) $

$ + (z-\mu_z)^T\left(P_{zz}^{-1} + P_{zz}^{-1}P_{zx}D^{-1}P_{xz}P_{zz}^{-1}\right)(z-\mu_z) - (z - \mu_z)^T P_{zz}^{-1} (z - \mu_z) $

Cancel $(z - \mu_z)^T P_{zz}^{-1} (z - \mu_z)$ out.

$ = (x - \mu_x)^T D^{-1} (x - \mu_x) - (x - \mu_x)^T D^{-1}P_{xz}P_{zz}^{-1} (z - \mu_z) - (z - \mu_z)^T P_{zz}^{-1}P_{zx}D^{-1}(x - \mu_x) $

$ + (z-\mu_z)^T\left(P_{zz}^{-1}P_{zx}D^{-1}P_{xz}P_{zz}^{-1}\right)(z-\mu_z) $

$ = \left[(x - \mu_x) - P_{xz}P_{zz}^{-1}(z-\mu_z) \right]^T D^{-1} \left[(x - \mu_x) - P_{xz}P_{zz}^{-1}(z-\mu_z) \right] $

$ = \left[x - (\mu_x + P_{xz}P_{zz}^{-1}(z-\mu_z)) \right]^T D^{-1} \left[(x - (\mu_x + P_{xz}P_{zz}^{-1}(z-\mu_z)) \right] $

$ = \left[x - \mu_{x \mid z} \right]^T P_{x \mid z}^{-1} \left[(x - \mu_{x \mid z} \right] $

Therefore

\begin{align} \mu_{x \mid z} = \mu_x + P_{xz}P_{zz}^{-1}(z-\mu_z) \end{align}

\begin{align} P_{x \mid z} = D = P_{xx} - P_{xz}P_{zz}^{-1}P_{zx} \end{align}
