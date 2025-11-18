---
layout: post
title:  "Waveguide Mode Orthogonality is an Eigenvalue Problem"
date:   2025-11-18 01:00:00 -0500
categories: Engineering
katex: True
excerpt_separator: <!--more-->
author: "Ryan Wans"
comments: True
---
We provide a short exposition on the connections between mode orthogonality in waveguides/resonators and the spectrum of linear operators in the context of electromagnetic theory.
<!--more-->

---
<br>

Here, we give a short exposition showing that orthogonality of electromagnetic modes follows directly from the fact that the curl–curl operator is Hermitian in a lossless, isotropic medium.

As usual, the intention here is not to emphasize applications, but rather to highlight a clean mathematical structure in Maxwellian theory.

Consider the case of a linear, isotropic, homogeneous, and non-dispersive medium such that $\mu$ and $\epsilon$ are real, positive scalars. Since Maxwell's equations satisfy the vector Helmholtz equation

$$\nabla \times \left( \frac{1}{\mu}\, \nabla \times \mathbf{E}(\mathbf{r}) \right)
= \omega^{2} \varepsilon\, \mathbf{E}(\mathbf{r})$$

where after rearranging, we obtain the eigenvalue problem
$$\mathcal{L}\mathbf{E} = \omega^{2}\mu\varepsilon\, \mathbf{E} = k^{2}\mathbf{E},$$
having $\mathcal{L} = \nabla\times\nabla\times$, as in equation (22.1.6) of [1]. By inspection, eigenfunctions $\textbf{E}(\textbf{r})$ have eigenvalue $k^2 = \omega^2\mu\epsilon$. We show below that, in the context of this lossless medium, our linear operator $\mathcal{L}$, which can be represented as a matrix, is Hermitian (self-adjoint).
    
<blockquote>
<b>Claim 1.</b> If $\mu$ and $\epsilon$ are real positive scalars, linear operator $\mathcal{L}$ is self-adjoint. 
</blockquote>
<proof>
    <i>Proof.</i>
    We aim to show that $\langle\textbf{A},\mathcal{L}\textbf{B}\rangle = \langle\mathcal{L}\textbf{A},\textbf{B}\rangle$. Assuming some smoothness conditions on vector field $\textbf{A}$ and $\textbf{B}$, we have that
    $$ \int_\Omega \textbf{A} \cdot (\nabla\times\textbf{B}) d\Omega = \int_\Omega (\nabla\times\textbf{A})\cdot\textbf{B} + \int_{\partial\Omega} (\hat{n}\times\textbf{A})\cdot\textbf{B} dS.$$
    Applying this identity twice and assuming PEC waveguide/resonator walls (boundary conditions provide us $\hat{n}\times\textbf{E} = 0$) yields exactly 
    $$\int_\Omega \textbf{A}^* \cdot (\nabla\times\nabla\times\textbf{B}) d\Omega = \int_\Omega (\nabla\times\nabla\times\textbf{A})^* \cdot \textbf{B}d\Omega,$$
    and hence $\mathcal{L}$ is Hermitian/self-adjoint ($\mathcal{L}^\dagger = \mathcal{L}$).
    <end>$\blacksquare$</end> 
</proof>

Now the result we've been waiting for :)

<blockquote>
<b>Claim 2.</b> Distinct modes in a waveguide/resonate are orthogonal.
</blockquote>
<proof>
    <i>Proof.</i>
    Consider two modes $\textbf{E}_m$ and $\textbf{E}_n$ with frequencies $\omega_n$ and $\omega_m$, respectively. Then we have that $\mathcal{L}\textbf{E}_m = k_m^2\textbf{E}_m$ and $\mathcal{L}\textbf{E}_n = k_n^2\textbf{E}_n$ by before. By self-adjointness,

    $$ \langle\textbf{E}_n,\mathcal{L}\textbf{E}_m\rangle = \langle\mathcal{L}\textbf{E}_n,\textbf{E}_m\rangle = k_n^2 \langle\textbf{E}_n,\textbf{E}_m\rangle= k_m^2\langle\textbf{E}_n,\textbf{E}_m\rangle$$

    and hence subtracting the two, we get 
    $$(k_m^2 - k_n^2)\langle\textbf{E}_n,\textbf{E}_m\rangle = 0.$$
    Hence $k_m\neq k_n \implies \langle\textbf{E}_n,\textbf{E}_m\rangle = 0$, which is analogous to $(\lambda_m - \lambda_n)\textbf{v}^\dagger_m\textbf{v}_n = 0$ as in (26.2.11) of [1].
    <end>$\blacksquare$</end> 
</proof>

Now I'm now going to restate the problem in terms of Section 22.2.1 of [1], which is a lot more interesting in terms of spectral theory! Consider the bounded cross-section $S$ of a hollow waveguide with smooth boundary $C = \partial S$. In the TE case of $H_z \neq 0$, we've that $(\nabla_s^2 + \beta_s^2)\Psi_s(\textbf{r}_s) = 0$ in $S$ and $\partial_n\Psi_s(\textbf{r}_s) = 0$ on $C$. We recognize this immediately as the Laplacian eigenvalue problem!

$$ -\nabla_s^2\Psi_s = \lambda_s\Psi_s,\qquad \lambda_s = \beta_s^2$$

Let's operate on some safe assumptions here. First, $S$ is bounded and sufficiently regular such that Green identities, etc hold. We'll assume Neumman boundary conditions such that $\partial_n\Psi_s = 0$ on the entire boundary $C$. Lastly, $\Psi_s$ is sufficiently smooth, so maybe let $\Psi_s \in L^2(S)$. Then the Laplacian $-\nabla_s^2$ with Neumann boundary conditions is self-adjoint, positive semi-definite, and $L^2(S)$ is $-\nabla_s^2$-stable.

<blockquote>
<b>Claim 3.</b> Distinct potential scalar potential modes $\Psi_{m}$ and $\Psi_n$ are orthogonal.
</blockquote>
<proof>
    <i>Proof.</i> 
    We have that
    $$ -\nabla_s^2\Psi_m = \beta_m^2\Psi_m,\qquad -\nabla_s^2\Psi_n = \beta_n^2\Psi_n $$
    where multiplying by $\Psi_n^*$ and integrating over $\Omega = S$ gives us
    $$ \int_S\Psi_n^*(-\nabla_s^2\Psi_m) dS = \beta_m^2\int_S \Psi_n^*\Psi_m dS. $$
    Performing the same with $n \rightleftarrows m$ and subtracting,
    $$ \int_S (\Psi_n^*(-\nabla_s^2\Psi_m) - \Psi_m(-\nabla_s^2\Psi_n)^*) dS = (\beta_m^2 - \beta_n^2) \int_S \Psi_n^*\Psi_m dS $$
    where, by Green's first identity, we have
    $$ \int_S (\Psi_n^*(-\nabla_s^2\Psi_m) - \Psi_m(-\nabla_s^2\Psi_n)^*) dS = \int_{\partial S} (\Psi_n^2\partial_n\Psi_m - \Psi_m\partial_n\Psi_n^*) dl. $$
    Now we can invoke our boundary conditions, where $\partial_n\Psi_m = \partial_n\Psi_m = 0$, so
    $$ (\beta_m^2 - \beta_n^2) \int_S \Psi_n^*(\textbf{r})\Psi_m(\textbf{r}) dS = 0 $$
    and hence $\beta_n^2 \neq \beta_m^2$ implies that $\langle\Psi_n,\Psi_m\rangle = 0$. Finally, when $\lambda = \beta^2 = 0$, then $\Psi_0(\textbf{r})$ is fixed constant, and we get that 
    $$ (0 - \beta_m^2) \int_S \Psi_0^*(\textbf{r})\Psi_m(\textbf{r}) dS = 0\quad \implies \quad \int_S\Psi_n dS = 0, $$
    so all modes are orthogonal to the constant mode. The entire spectrum is nonnegative when $\omega$, $\mu$, and $\varepsilon$ are all real.
    <end>$\blacksquare$</end>
</proof>
    
This result warrants some further spectral analysis, which I may explore in the future.
<br><br>
<references>
<start>References</start>

&#8291;1. W. C. Chew, <i>Lectures on Electromagnetic Field Theory</i>, 1st edition, 2024.
<references>
