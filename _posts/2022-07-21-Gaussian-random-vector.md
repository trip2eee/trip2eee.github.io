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

Let $x \sim \mathcal{N}\left(\mu_x, P_{xx}\right)$ and $z \sim \mathcal{N}\left(\mu_z, P_{zz}\right)$ are jointly normally distributed.

\begin{align} y = \begin{bmatrix} x \\\\ z \end{bmatrix} \end{align}

\begin{align} P_{yy} = \begin{bmatrix} P_{xx} & P_{xz} \\\\ P_{zx} & P_{zz} \end{bmatrix} \label{eq_pyy}\end{align}


Then the conditional pdf of $X$ can be given as follows

\begin{align} p_{x \mid z} (x \mid z) = \frac{p_{xz}(x,z)}{p_z(z)} = \frac{p_y(y)}{p_z(z)} \end{align}

\begin{align} = \frac{p_{xz}(x,z)}{p_z(z)} = \frac{p_y(y)}{p_z(z)} \end{align}

\begin{align} = \frac{\sqrt{(2\pi)^p detP_{zz}}}{\sqrt{(2\pi)^{n+p}det P_{yy}}} exp\left( -\frac{1}{2} \left\\{  (y-\mu_y)^T P_{yy}^{-1} (y-\mu_y) - (z-\mu_z)^T P_{zz}^{-1} (z-\mu_z) \right\\} \right) \label{eq_pxz}\end{align}

where $n$ and $p$ are dimensions of $z$ and $z$.

Then the inverse of Eq.$\ref{eq_pyy}$ can also be expressed in the matrix form.

\begin{align} P_{yy}^{-1} = \begin{bmatrix} D^{-1} & -D^{-1} P_{xz} P_{zz}^{-1} \\\\ -P_{zz}^{-1}P_{zx}D^{-1} & P_{zz}^{-1}+P_{zz}^{-1}P_{zx}D^{-1}P_{xz}P_{zz}^{-1} \end{bmatrix} \end{align}

where

\begin{align}D = P_{xx} - P_{xz}P_{zz}^{-1}P_{zx} \end{align}

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