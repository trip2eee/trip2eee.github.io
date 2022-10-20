---
layout: post
title: "Glossary of topology"
categories: "Math"
tags: [Topology]
use_math: true
comments: true
---

# Glossary of topology

## Functions
### A function $f: A \rightarrow B$
#### injective (one-to-one)
For each pair of distinct point of A, their images under f are distinct.
#### surjective (A onto B)
Every element of B is the image of some element of A under the function f.
#### bijective (one-to-one correspondence)
$f$ is both injective and surjective

## Finite Sets
### Countable and Uncountable Sets
A set $A$ is said to be infinite if it is not finite.
It is said to be countably infinite if there is a bijective correspondence.

$f: A \rightarrow Z_{+}$

A set is said to be countable if it is either finite or countably infinite. A set that is not countable is said to be uncountable.

## The Subspace Topology
### subspace topology
Let $X$ be a topological space with topology $\mathscr{T}$. If $Y$ is a subset of X, then collection

$\mathscr{T}_Y = \{Y \cap U \mid U \in \mathscr{T} \}$

is a topology on $Y$, called the subspace topology.

## Closed Sets and Limit Points
### Closed Sets
A subset $A$ of a topological space $X$ is said to be closed if the set $X-A$ is open.

#### Example
The subset $\left[a, b\right]$ of $\mathbb{R}$ is closed because its complement $\mathbb{R}-\left[a,b\right] = \left(-\infty, a\right) \cup \left(b, \infty\right)$ is open.

Similarly, $[a, +\infty)$ is closed, because its complement $\left(-\infty, a\right)$ is open. 

The subset $[a, b)$ of $\mathbb{R}$ is neither open nor closed.

If $Y$ is a subspace of $X$, we say that a set $A$ is closed in $Y$ if $A$ is a subset of $Y$ and if $A$ is closed in the subspace topology of $Y$ (that is, $Y-A$ is open in $Y$).

### Open in $X$



# Reference
[1] James Munkres, Topology Second Edition, Pearson(2014)

[2] https://en.wikipedia.org/wiki/Glossary_of_topology