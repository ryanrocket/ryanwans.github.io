---
layout: post
title:  "Interesting Property of Binomial Distributions"
date:   2024-10-10 01:00:00 -0500
categories: maths, ece
katex: True
excerpt_separator: <!--more-->
author: "Ryan Wans"
comments: True
published: False
---
Observing the behavior of $B(n, p)$ for $np \in \mathbb{Z}$.
<!--more-->

---
<br>

We have the following proposition, which seems deceptively simple and intuitive, but is actually quite interesting. 

<blockquote>
<b>Proposition.</b> Given $X \sim B(n, p)$ and $np \in \mathbb{Z}$, we have that 
$$
\mathbb{E}[X] = \text{Median}(X) = \text{Mode}(X) = np.
$$
</blockquote>

This is a very interesting property of the binomial distribution. It is clear that the expected value of $X$ is $np$, but the fact that the median and mode are also $np$ is quite intriguing. I will provide a proof of this proposition... eventually. My guess is that the case where $p \in \mathbb{Z}$ is trivial, but I will have to think about the case where $p \notin \mathbb{Z}$. ~~Updates to come~~. 

I now have a proof for this. An outline was originaly provided in $[1]$ from what I believe to be from 2010. A mistake arises in the proof, which the author recognizes in $[2]$ but has not corrected. I will provide a corrected proof. This problem has since been solved by Boyan Zhang in $[3]$. I also credit him with recognizing the mistake in the first place. 

<proof>
<i>Proof.</i> 
We will start by examining the case for $0 < p < 1$, and evaluate the boundary points at the end. First, we define the mode for any distribution 

$$
\renewcommand{\P}[1]{\mathbb{P}\left[ #1 \right]}
\text{Mode}(X) = \max_{k\in\text{Supp}(X)}\left\{ \P{X = k} \right\}.
$$

We will use a ratio of consecutive probabilities as used in $[1]$ to prove that $k = np$ has the largest probability. Let $k \in \text{Supp}(X)$ and $q = 1 - p$. We have that
$$
\renewcommand{\P}[1]{\mathbb{P}\left[ #1 \right]}
    \frac{\P{X = k}}{\P{X = k - 1}} \equiv 
    \frac{\displaystyle \binom{n}{k}p^kq^{n-k}}{\displaystyle \binom{n}{k-1}p^{k-1}q^{n-k+1}} = 
    \frac{n-k+1}{k}\cdot\frac{p}{1-p}.
$$
When $k \leq np$ this value is greater than 1, and when $k \geq np + 1$ it is less than 1. In other words, values before and after $np$ are less likely to occur, meaning $np$ has the largest probability. Thus, we have that $\text{Mode}(X) = np$, as confirmed in $[1]$.  We continue into the portion of the proof which is flawed; establishing the median. The median of any distribution is given by the value $k$ for which
$$
\renewcommand{\P}[1]{\mathbb{P}\left[ #1 \right]}
\P{X \geq k} \geq \frac{1}{2},\quad \P{X \leq k} \geq \frac{1}{2}.
$$
This can be interpreted as the point $k$ at which the probability of $n$ being greater than or less than $k$ is equal, and equal to one half. Observe the following;
$$
\renewcommand{\P}[1]{\mathbb{P}\left[ #1 \right]}
\sum_{r=0}^{np}\P{X = r} = \sum_{r=0}^{n(p-q)}\P{X = r} + \sum_{k=1}^{nq}\P{X = np - k + 1}. \tag{1}
$$
We are splitting the discrete sum $0 \to np$ into $0 \to n(p-q) > 0$ and $n(p-q) + 1 \to np$. 
<blockquote>
<b>Claim 1.1.</b> We make that claim that, given $p \geq q$,

$$
\renewcommand{\P}[1]{\mathbb{P}\left[ #1 \right]}
\P{X = np + k} < \P{X = np - k + 1}
$$
for some $k \in [1, nq]$. 
</blockquote>

Given this, it would then follow from equation $(1)$ that
$$
\renewcommand{\P}[1]{\mathbb{P}\left[ #1 \right]}
\sum_{r=0}^{np}\P{X = r} > \sum_{k=1}^{nq}\P{X = np + k} = \sum_{r=np+1}^n \P{X = r}, \tag{2}
$$
which is equivalent to proving the first half of the median condition. It is at this point in the original proof that they swap $p \leftrightarrow q$ and claim that the second half of the median condition is satisfied. This, however, fails since the proof of <b>Claim 1.1</b> hinges on the condition that $p \geq q$. Thus $[1]$ has effectively only proven the case for $p = q = 1/2$. The goal was to show that,
$$
\renewcommand{\P}[1]{\mathbb{P}\left[ #1 \right]}
\sum_{r=np}^n \P{X = r} > \sum_{r=0}^{np-1} \P{X = r},
$$
which would complete the proof for the median. Attempting to swap $p \leftrightarrow q$ results in,
$$
\renewcommand{\P}[1]{\mathbb{P}\left[ #1 \right]}
\sum_{r=0}^{nq}\P{X = r} = \boxed{\sum_{r=0}^{n(q-p)}\P{X = r}} + \sum_{k = 1}^{np}\P{X = nq - k + 1}, \\ 
\sum_{r=0}^{nq}\P{X = r} = \sum_{k = 1}^{np}\P{X = nq - k + 1}.
$$
We can no longer apply <b>Claim 1.1</b> to the second equality to make it into the goal form aforementioned. Moreover, the boxed sum in this case is strictly zero, whereas in the original case it was greater than or equal to zero. Boyan Zhang completes the proof in $[3]$. His proof relies on finding an associated $Y \sim \text{Beta}(\alpha, \beta)$ which has the structure $mean \leq median \leq mode$. Since we have already established well-defined values for the mean and mode, we can use this structure to claim bounds on the median, which must be $np$.<br><br>

As promised, we cover the case for $p \in \mathbb{Z}$. This is left as an exercise to the reader.
<end>$\blacksquare$</end>
</proof>

### An Intuitive Approach

So we have some $X \sim B(n, p)$ with $(np) \in Z$. We are flipping a coin which has the probability of heads $p$ some $n$ times. We are studying how many times we get heads after running this $n-\text{Bernoulli}$ trial. We take the expectation of $X$ at face value; on average, we expect to get $np$-many heads. But why are the median and mode also $np$?

First, it makes sense that these numbers are integers. The median is the value for which half of the probability mass is to the left and half is to the right. If $np$ is not an integer, then the median would be the average of the two closest integers. But this would mean that the probability mass is not evenly distributed, which is a contradiction. Remember, we are dealing with a discrete distribution. 

The mode is the value which has the highest probability of occuring. If $np$ is not an integer, then then that probability mass is not concentrated at a single point, which is again a contradiction to the notion of a discrete distribution.

<references>
<start>References</start>

&#8291;1. Nick Lord, <i>Binomial averages when the mean is an integer,</i> <b>94</b>, no. 530, 331-332.<br>

&#8291;2. Nick Lord, <i>Binomial averages: an erratum,</i> The Mathematical Gazette. 2013;97(539):336-336.<br>

&#8291;3. Boyan Zhang, <i>For Binomial(n,p), if np is an integer, mean=median=mode</i>. Not yet public.
<references>