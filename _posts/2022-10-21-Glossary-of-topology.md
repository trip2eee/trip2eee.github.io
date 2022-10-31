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
For each pair of distinct point of $A$, their images under $f$ are distinct.
#### surjective (A onto B)
Every element of $B$ is the image of some element of $A$ under the function $f$.
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


## The Fundamental Group
### Homotopic
If $f$ and $f'$ are continuous maps of the space $X$ into the space $Y$, we say that $f$ is homotopic to $f'$ if there is a continuous map $F: X \times I \rightarrow Y$ such that 

$F(x, 0)=f(x)$ and $F(x,1)=f'(x)$

for each $x$. Where $I=[0,1]$. The map $F$ is called a homotopy between $f$ and $f'$. If $f$ is homotopic to $f'$, we write $f \simeq f'$.

### Nullhomotopic
If $f \simeq f'$ and $f'$ is constant map, we say that $f$ is nullhomotopic.

### initial point and final point
If $f:[0,1] \rightarrow X$ is a continuous map such that $f(0) = x_0$ and $f(1) = x_1$, we say that $f$ is a path in $X$ from $x_0$ to $x_1$. We also say that $x_0$ is the initial point, and $x_1$ the final point of the path $f$.

### Path homotopic
Two paths $f$ and $f'$, mapping the interval $I = [0,1]$ into $X$, are said to be path homotopic if they have the same initial point $x_0$ and the same final point $x_1$, and if there is a continuous map $F:I \times I \rightarrow X$ such that

$F(s,0) = f(s)$ and $F(s,1) = f'(s)$,

$F(0,t) = x_0$ and $F(1,t) = x_1$,

for each $s \in I$ and $t \in I$. We call $F$ a path homotopy between $f$ and $f'$ ($f \simeq_p f'$).

### product
If $f$ is a path in $X$ from $x_0$ to $x_1$, and if $g$ is a path in $X$ from $x_1$ and $x_2$, we define the product $h = f*g$ by the equations
$$
\begin{align}
h(s) = 
\begin{cases} 
	f(2s) & \text{for } s \in \left[0, \frac{1}{2}\right] \\
	g(2s-1) & \text{for } s \in \left[\frac{1}{2}, 1\right]
\end{cases}
\end{align}
$$

#### The property of the operation *
- Associativity: If $[f]\*([g]\*[h])$ is defined, so is $([f]\*[g])\*[h]$, and they are equal.
- Right and left identities: Given $x \in X$, let $e_x$ denote the constant path $e_x:I \rightarrow X$ carrying all of $I$ to the point $x$. If $f$ is a path in $X$ from $x_0$ to $x_1$, then $[f]\*[e_{x_1}]=[f]$ and $[e_{x_0}]\*[f]=[f]$.
- Inverse: Given the path $f$ in $X$ from $x_0$ to $x_1$, let $\bar{f}$ be the path defined by $\bar{f}(s)=f(1-s)$. It is called the reverse of $f$. Then $[f]\*[\bar{f}]=[e_{x_0}]$ and $[\bar{f}]\*[f]=[e_{x_1}]$.

#### positive linear map of $[a,b]$ to $[c,d]$
If $[a,b]$ and $[c,d]$ are two intervals in $\mathbb{R}$, there is a unique map $p:[a,b] \rightarrow [c,d]$ that carries $a$ to $c$ and $b$ to $d$; we call it the positive linear map of $[a,b]$ to $[c,d]$.

### The Fundamental Group
Let's suppose we pick out a point $x_0$ of $X$ to serve as a "base point" and restrict ourselves to those paths that begin and end at $x_0$. The set of theese path-homotopy classes does form a group under *. It will be called the fundamental group of $X$.

Let's suppose $G$ and $G'$ are groups. A homeomorphism $f: G\rightarrow G'$ is a map such that $f(x\cdot y)=f(x)\cdot f(y)$ for all $x$, $y$; it automatically satisfies the equations $f(e)=e'$ and $f\left(x^{-1}\right)=f^{-1}(x)$, where $e$ and $e'$ are the identies of $G$ and $G'$, respectively, and the exponent -1 denotes the inverse. The kernel of $f$ is thet set $f^{-1}\left(e'\right)$; it is a subgroup of $G$. The image of $f$, similarly, is a subgroup of $G'$. 
- Monomorphism: The homomorphism of $f$ is injective. 
- Epimorphism: The homomorphism of $f$ is surjective
- Isomorphism: The homomorphism of $f$ is bijective.

#### loop
Let $X$ be a space; let $x_0$ be a point of $X$. A path in $X$ that begins and ends at $x_0$ is called a loop based at $x_0$. The set of path homotopy classes of loops based at $x_0$, with the operation *, is called the fundamental group of $X$ relative to the base point $x_0$. It is denoted by $\pi_1\left(X, x_0\right)$

#### simply connected
A space $X$ is said to be simply connected if it is a path-connected space and if $\pi_1\left(X,x_0\right)$ is the trivial (one-element) group for some $x_0 \in X$, and hence for every $x_0 in X$. We often express the fact that $\pi_1\left(X, x_0\right)$ is the trivial group by writing $\pi_1\left(X, x_0\right)=0$.

#### homomorphism induced by $h$
Let $h:(X,x_0) \rightarrow (Y,y_0)$ be a continuous map. Define

$h_*:\pi_1(X,x_0) \rightarrow \pi_1(Y,y_0)$

by the equation

$h_*\left([f]\right) = [h \circ f]$

The map $h_*$ is called the homomorphism induced by $h$, relative to the base poitn $x_0$.

### Convering Spaces
#### evenly covered
Let $p:E\rightarrow B$ be a continuous surjective map. The open set $U$ and $B$ is said to be evenly covered by $p$ if the inverse image $p^{-1}(U)$  can be written as the union of disjoint open sts $V_\alpha$ in $E$ such that for each $\alpha$, the restriction of $p$ to $V_\alpha$ is a homeomorphism of $V_\alpha$ onto $U$. The collection $\{V_\alpha\}$ will be called a partition of $p^{-1}(U)$ into slices.

#### coveringmap and coveringspace
Let $p: E \rightarrow B$ be continuous and surjective. If every point $b$ of $B$ has a neighborhood $U$ that is evenly covered by $p$, then $p$ is called coveringmap, and $E$ is said to be a converingspace of $B$.

## The Seifert-van Kampen Theorem
### Abelian Groups
In mathematics, an abelian group, also called a commutative group, is a group in which the result of applying the group operation to two group elements does not depend on the order in which they are written. That is, the group operation is commutative.

# Reference
[1] James Munkres, Topology Second Edition, Pearson(2014)

[2] https://en.wikipedia.org/wiki/Glossary_of_topology

[3] https://en.wikipedia.org/wiki/Abelian_group