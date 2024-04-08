---
layout: post
title: Some Analysis on Sigma Algebra
subtitle: Probability Theory and Mathematical Statistics
date: 2024-04-03
categories: test
tags: math courses 
---



*As we know, sigma algebra is the basis of probability theory. Let's delve in it and look at some typical problems...*

### Definition

> Assume $\Omega$ is a sample space. A collection $\mathcal{F}$ of subsets of $\Omega$ is called a **$\sigma$-field** (or **$\sigma$-algebra**) if it satisfies the following conditions:
>
> * **Empty set** : $\varnothing\in\mathcal{F}$.
> * **Closure under complement** : if $A\in\mathcal{F}$ then $A^\complement\in\mathcal{F}$.
> * **Closure under countable union** : for countable $A_1,A_2,\cdots\in\mathcal{F}$ then $\bigcup_{i=1}^\infty A_i\in\mathcal{F}$.

Obviously, $\sigma$-algebra is a kind of mathematical set operation structure. Whenever we need to verify that a structure is $\sigma$-algebra, we need to verify the three properties given in the definition.

#### Example 1

The smallest $\sigma$-field associated with $\Omega$ is the collection $\mathcal{F}=\{\varnothing, \Omega\}$.

#### Example 2

If $A$ is any subset of $\Omega$ then $\mathcal{F}=\{\varnothing,A,A^\complement,\Omega\}$ is a $\sigma$-field.

#### Example 3

The *power set* of $\Omega$, which is written $\{0,1\}^\Omega$ and contains all subsets of $\Omega$, is obviously a $\sigma$-field. For reasons beyond the scope of this book, when $\Omega$ is infinite, its power set is too large a collection for probabilities to be assigned reasonably to all its members.

------

### Problem 1

**[Nonexistence of Probability Space]**  Prove that it is impossible to define a uniform probability law on natural numbers $\mathbb{N}$. More precisely, prove that there does not exist a probability space $(\mathbb{N},2^\mathbb{N},\Pr)$ such that $\Pr(\{i\})=\Pr(\{j\})$ for all $i,j\in\mathbb{N}$. Please explain why the same argument fails to prove that there is no uniform probability law on the real interval $[0,1]$, that is, there is no such probability space $([0,1],\mathcal{F},\Pr)$ that for any interval $(l,r]\subseteq[0,1]$, it holds that $(l,r]\in\mathcal{F}$ and $\Pr((l,r])=r-l$. (Actually, such probability measure does exist and is called the Lebesgue measure on $[0,1]$).

#### Solution

First, we need to prove that it is impossible to define a uniform probability law on the set of natural numbers $\mathbb{N}$.

Assume that there exist a probability space $(\mathbb{N}, 2^\mathbb{N}, \Pr)$ such that $\Pr(\{i\})=\Pr(\{j\})$ for all $i,j\in \mathbb{N}$. Consider the total probability of the entire sample space $\mathbb{N}$: $\Pr(\mathbb{N})=\Pr(\{1\})+\Pr(\{2\})+\cdots$. Since each singleton set has the same probability, let's denote this common probability as $p$. Give n that $\Pr(\mathbb{N})=1$ (as it is a probability measure over the entire sample space), we have $1=p+p+\cdots=\infty\cdot p$. This equation implies that $p=0$, because otherwise the sum would diverge. However, this means that the probability of every singleton set in $\mathbb{N}$ is zero. Yet, by the countable additivity property of probability measures, we know that $\sum_{i}\Pr(\{i\})=\sum_i0=0$, which contradicts to the one-summation rule. Therefore, our assumption that a uniform probability law exists on $\mathbb{N}$ must be false.

For the second statement, proving that there is no uniform probability law on the real interval $[0,1]$, the same argument cannot be used because the real interval $[0,1]$ is uncountably infinite, whereas the set of natural numbers $\mathbb{N}$ is countably infinite.

We have used an important property from mathematical analysis. It states that the sum of a countable number of zeros is always zero, while the sum of an infinite uncountable number of zeros is indeterminate. In fact, for the real interval [0,1], probability (measure) can be defined using geometric probability models, which implies that $\Pr(\left(l,r\right])=r-l$ for any intervals $\left(l,r\right]\subseteq[0,1]$.

### Problem 2

**[Smallest $\sigma$-Field]**  For nay subset $S\subseteq2^\Omega$, prove that the smallest $\sigma$-field containing $S$ is given by $\bigcap_{S\subseteq\mathcal{F}\subseteq2^\Omega}\mathcal{F}$, where $\mathcal{F}$ is a $\sigma$-field.

#### Solution

Let $\mathcal{F}_{\alpha}$, where $\alpha$ is an index set, be a collection of $\sigma$-fields containing $S$. First, We need to prove $\mathcal{F}=\bigcap_{\alpha}\mathcal{F}_{\alpha}$ is itself a $\sigma$-field.

- Empty set. Trivially, since for all $\alpha$,  $\mathcal{F}_\alpha$ contains empty set. 
- Closure under complement. Let $A\in\mathcal{F}$, then $A\in\mathcal{F}_{\alpha}$ for all $\alpha$. Since each $\mathcal{F}_{\alpha}$ is a $\sigma$-field, $A^\complement\in\mathcal{F}_{\alpha}$ for all $\alpha$. Thus, $A^\complement\in\mathcal{F}$.
- Closure under countable union. Let $A_1,A_2,\cdots\in\mathcal{F}$. Then, $A_i \in \mathcal{F}_{\alpha}$ for all $\alpha$. Since each $\mathcal{F}_\alpha$ is a $\sigma$-field, $\bigcup_{i} A_i \in \mathcal{F}_{\alpha}$ for all $\alpha$. Thus, $\bigcup_{i}A_i \in \mathcal{F}$.

These three basic rules determine that $\mathcal{F}$ is a $\sigma$-field. Second, we need to prove that $\mathcal{F}$ is the smallest $\sigma$-field containing $S$. Let $\mathcal{G}$ be any $\sigma$-field containing $S$, i.e. $S\subseteq\mathcal{G}$. Since $\mathcal{F}$ is defined as the intersection of all such $\sigma$-fields containing $S$, it follows that $\mathcal{F}\subseteq\mathcal{G}$, which means that $\mathcal{F}$ is the smallest $\sigma$-field containing $S$.

Therefore, we have shown both parts, and hence proved that the smallest $\sigma$-field containing $S$ is given by $\mathcal{F}$, i.e. the intersection of all $\sigma$-fields containing $S$.

### Problem 3

**[Union of $\sigma$-field]**  Let $\mathcal{F}$ and $\mathcal{G}$ be $\sigma$-fields of subsets of $\Omega$. Show that $\mathcal{F}\cup\mathcal{G}$ is not necessarily a $\sigma$-field.

#### Solution

The union of two $\sigma$-fields is not necessarily a $\sigma$-field. Intuitively, let two subsets $A,B\subseteq\Omega$, the according smallest $\sigma-$fields are $\mathcal{F}=\{\varnothing, \Omega, A, A^\complement\}$ and $\mathcal{G}=\{\varnothing, \Omega, B, B^\complement\}$. However, their union $\mathcal{F}\cup\mathcal{G}=\{\varnothing, \Omega, A, B, A^\complement, B^\complement\}$ is NOT a $\sigma$-field because the closure under countable union does not hold any more. For instance, $A\cup B\notin\mathcal{F}\cup\mathcal{G}$ for any time.

### Problem 4

**[Probability space?]** Let $\Omega=\mathbb{R}$, $\mathcal{F}$ is the set of all subsets $A\subseteq\Omega$ so that $A$ or $A^\complement$ is countable, $\Pr(A)=0$ in the first case and $\Pr(A)=1$ in the second. Is $(\Omega,\mathcal{F},\Pr)$ a probability space? Please explain your answer.

#### Solution

$(\Omega,\mathcal{F},\Pr)$ is a probability space. Here's the proof. First, we need to show that $(\Omega, \mathcal{F})$ is a $\sigma$-field.
	
Denote that $\mathcal{F}=\mathcal{F}_1\cup\mathcal{F}_2$, where $\mathcal{F}_1=\{A\in\Omega: A \text{ is countable}\}$ and $\mathcal{F}_2=\{A\in\Omega :A^C \text{ is countable}\}$.

- Empty set. Trivially, since $\emptyset\in\mathcal{F}_1\subseteq\mathcal{F}$.
- Closure under complement. For countable set $A\in\Omega$, we have $A\in\mathcal{F}_1$, its complement $A^C\in\mathcal{F}_2$. For countable set $B^C\in\Omega$, we have $B^C\in\mathcal{F}_1$, its complement $(B^C)^C=B\in\mathcal{F}_2$. 
- Closure under countable union. Suppose that $A_1, A_2,\cdots$ is a sequence of sets in $\mathcal{F}$. If for all $i\in\mathbb{N}^*$, $A_i\in\mathcal{F}_1$, then $\bigcup_{i}A_i$ is countable union of countable sets, thus countable, so $\bigcup_iA_i\in\mathcal{F}_1\subseteq\mathcal{F}$. Otherwise, these exist $i_0\in\mathbb{N}^*$ such that $A_{i_0}\in\mathcal{F}_2$, thus $(\bigcup_iA_i)^C\subseteq A_{i_0}^C$ is a subset of a countable set, thus countable, so $\bigcup_iA_i\in\mathcal{F}_2\subseteq\mathcal{F}$.

We managed to prove that $(\Omega, \mathcal{F})$ is a $\sigma$-field. Then we should to deal with $\Pr$. Notice that $\mathcal{F}_1\cap\mathcal{F}_2=\emptyset$, which guarantee that $\Pr$ is well-defined. In fact, since $\Omega=\mathbb{R}$ is not countable(whose cardinality is $\aleph$), for any $A\in\mathcal{F}_1\cap\mathcal{F}_2$, we have that $\Omega=A\cup A^C$ is countable, leads to a contradiction.

Suppose that $A_1,A_2,\cdots$ is a sequence of disjoint sets in $\mathcal{F}$. If for all $i\in\mathbb{N}^*$, $A_i\in\mathcal{F}_1$, as we proved $\bigcup_iA_i\in\mathcal{F}_1$, thus $\Pr(\bigcup_iA_i)=0=\sum_i0=\sum_i\Pr(A_i)$. Otherwise, suppose that $i_0\in\mathbb{N}^*$ satisfies that $A_{i_0}\in\mathcal{F}_2$, then for any $i\neq i_0*$, suppose that $A_i\in\mathcal{F_2}$, since $A_i\cap A_{i_0}=\emptyset$, we have $\Omega=\emptyset^C=(A_i\cap A_{i_0})^C=A_i^C\cup A_{i_0}^C$ is an union of two countable sets, thus countable, leads to a contradiction. Therefore $A_i\in\mathcal{F}_1$ for $i\neq i_0$. As proved previously, $\bigcup_iA_i\in\mathcal{F}_2$. Therefore, we have

$$\Pr(\bigcup_iA_i)=1=1+0=1+\sum_{i\neq i_0}0=\Pr(A_{i_0})+\sum_{i\neq i_0}\Pr(A_i)=\sum_i\Pr(A_i).$$

Plus, trivially we have $\Pr(\Omega)=1$, because $\Omega=\mathbb{R}$ is uncountable. Finally we proved that $(\Omega, \mathcal{F}, \Pr)$ is exactly a probability space.

### Problem 5

**[$\sigma$-field?]** A set $A\in\mathbb{N}$ is said to have asymptotic density $\theta$ if
$$
\lim_{n\rightarrow\infty}\frac{|A\cap\{1,2,\cdots,n\}|}{n}=\theta.
$$
Let $\mathcal{A}$ be the collection of sets for which the asymptotic density exists. Is $\mathcal{A}$ a $\sigma$-algebra? Please explain your answer.

#### Solution 

Let $A$ be the set of even numbers. Then $A\in\mathcal{A}$ with $\theta=1/2$/ Let $I_0=\{1\},I_k=\{n|2^{k-1}<n\leq2^k\}$, for $k=1,2,\cdots$. Construct $B$ as follows:

$$
B=\bigcup_{k=0}^\infty\{(I_{2k}\cap A^C)\cup(I_{2k+1}\cap A)\}.
$$
Then $B\in\mathcal{A}$ with $\theta=1/2$, since we only extract half of the elements from every $I_k$($k\geq2$). However, $A\cap B\notin\mathcal{A}$ for following reasons.

First, consider $n=2^{2m}$, we have that

$$
\begin{align*}
    \frac{|(A\cap B)\cap\{1,2,\cdots,2^{2m}\}|}{2^{2m}}&=\frac{1}{2^{2m}}\sum_{k=1}^m\frac{1}{2}|I_{2k-1}|\\
    &=\frac{1}{2^{2m}}\left(1+\sum_{k=2}^m2^{2k-3}\right) \\
    &=\frac{1}{2^{2m}}\cdot\frac{2^{2m-1}+1}{3}\rightarrow\frac{1}{6}.
\end{align*}
$$

Second, we consider $n=2^{2m+1}$, we have that

$$
\begin{align*}
    \frac{|(A\cap B)\cap\{1,2,\cdots,2^{2m+1}\}|}{2^{2m+1}}&=\frac{1}{2^{2m+1}}\sum_{k=1}^{m+1}\frac{1}{2}|I_{2k-1}|\\
    &=\frac{1}{2^{2m+1}}\left(1+\sum_{k=2}^{m+1}2^{2k-3}\right) \\
    &=\frac{1}{2^{2m+1}}\cdot\frac{2^{2m+1}+1}{3}\rightarrow\frac{1}{3}.
\end{align*}
$$

By the above two equations, we observe that $X=|(A\cap B)\cap\{1,2,\cdots n\}|/n $ satisfy $\limsup X\geq 1/3$ and $\liminf X\leq 1/6$, which means $\lim X$ does not exist. Therefore, $A\cap B\notin\mathcal{A}$, which implies that $\mathcal{A}$ is NOT a $\sigma$-algebra (even not an algebra).

##### I hope it helps!