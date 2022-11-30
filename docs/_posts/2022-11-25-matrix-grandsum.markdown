---
layout: post
title:  "On The Grand Sum of Matrices"
date:   2022-11-25 23:18:45 -0500
categories: maths
katex: True
excerpt_separator: <!--more-->
author: "Ryan Wans"
comments: True
---
Here's a little quirk I've recently stumbled upon. It seems as if the number of operations required to calculate the "grand sum" of a matrix is bounded by $n^2$ where $n$ is the order of the matrix. While this makes sense, let us explore some of the ways one can define this sum.
<!--more-->

---
<br>
The first method that comes to mind when pondering how to sum every term of a matrix would be to iteratively sum each element within. Suppose we have some matrix $\mathbb{A}$ such that:

$$ \mathbb{A} = \begin{bmatrix}
a_{11} & \cdots & a_{1n} \\
\vdots & \ddots & \vdots \\
a_{n1} & \cdots & a_{nn}
\end{bmatrix} \tag{1.1}$$

It would make sense to express the sum of said matrix as:

$$
\sum_{i=1}^{n}\sum_{j=1}^{n}a_{ij}
\tag{1.2}$$

where one can iterate over each row and column. This makes sense, but is indeed a cumbersome operation. As prefaced, $n^2$ operations would be needed to compute this. 

What's interesting, however, is that there a rather simple way to express this. 

<blockquote>
<b>Corollary</b> If the grand sum of some matrix $\mathbb{A}$ of order $n$ is defined in $(1.2)$, one can also express the grand sum as a product such that
$$\mathrm{grandsum}(\mathbb{A})=\textbf{e}^{T}\mathbb{A}\textbf{e}$$
where $\textbf{e}$ is the sum of the standard basis vectors $\sum_{i \in S}\textbf{e}_{i}$ in the vector space of $\mathbb{R}^n$.
</blockquote>

Let's explore this further. Suppose we start from the same matrix as defined in $(1.1)$ of some order $n$. 

$$
\mathbb{A}\textbf{e}=\begin{bmatrix}
a_{11} & \cdots & a_{1n} \\
\vdots & \ddots & \vdots \\
a_{n1} & \cdots & a_{nn}
\end{bmatrix}
\begin{bmatrix}
1 \\
\vdots \\
1 \\
\end{bmatrix} = 
\begin{bmatrix}
\sum_{j}a_{1j} \\
\vdots \\
\sum_{j}a_{nj} \\
\end{bmatrix}
\tag{1.3}$$

Then applying the transpose of $e$ to this result:

$$
\textbf{e}^{T}\mathbb{A}\textbf{e}=
\begin{bmatrix}
1 & \cdots & 1
\end{bmatrix}
\begin{bmatrix}
\sum_{k}a_{1k} \\
\vdots \\
\sum_{k}a_{nk} \\
\end{bmatrix} = 
\begin{bmatrix}
\sum_{i}\sum_{j}a_{ij}
\end{bmatrix}
\tag{1.4}$$

An identical result is shown. The corollary above provides an interesting way of looking at the grand sum operation. Though it is arguably much more intensive to compute at larger scales, it is certainly an intuitive way to observe what happens during the sum.

So how does the use of the grand sum compare to something like the trace $\mathrm{tr}(\mathbb{A})$ of a matrix? While it's not as widely used (or known), [this article](https://math.stackexchange.com/questions/4177851/what-does-the-grand-sum-of-a-linear-transformation-matrix-tell-us-about-its-acti) provides a great explaination of one of it's uses.

<note>
<b>Edited 11/29/2022:</b> Clarify what $\textbf{e}$ represents.
</note>