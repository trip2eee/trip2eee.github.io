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
### Closure and Interior of a Sets
Given a subset $A$ of a topological space $X$,
- The interior of $A$: The union of all open sets contained in $A$ ($Int A$).
- The closure of $A$: the intersection of all closed sets containing $A$ ($Cl A$ or $\bar{A}$).

### Limit Points
$x$ is a limit point of $A$ if it belongs to the closure of $A-{x}$.

$x$ is a limit point of $A$ if it belongs to the intersection of all closed sets containing of $A-{x}$.

The point $x$ may lie in $A$ or not.

## Continuous Functions
### Continuity of a Function
Let $X$ and $Y$ be topological spaces.A function $f:X \rightarrow Y$ is said to be continuous if for each open subset $V$ of $Y$, the set $f^{-1}(V)$ is an open subset of $X$.


## Homeomorphisms
Let $X$ and $Y$ be topological spaces; let $f:X \rightarrow Y$ be a bijection. If both the function $f$ and the inverse function

$f^{-1}: Y \rightarrow X$

are continuous, then $f$ is called a homeomorphism.

# Reference
[1] James Munkres, Topology Second Edition, Pearson(2014)

[2] https://en.wikipedia.org/wiki/Glossary_of_topology