---
layout: post
title: Probability Theory Problem-set 1
date: 2024-04-03
categories: test
tags: math courses 
---

<font color = 'red'>**There seems something wrong with the mathematical formulas... I will fix them up later... But if you are eager to see it, I feel sorry that you have to make do with it.**</font>

## Problem 1

![](https://github.com/llllllimitedX/tmpdatas/blob/main/img24/prps101.png?raw=true)

#### 1-1 Union Bound

The definition of probability space tells us that for disjoint events $A_1,A_2,\cdots\in\mathcal{F}$, we have $\Pr(\bigcup_iA_i)=\sum_i\Pr(A_i)$. Therefore, an intuition is that we can transform events $A_1,A_2,\cdots,A_n$ to disjoint events $B_1,B_2,\cdots,B_n$ where $B_1=A_1,B_2=A_2 \backslash A_1,B_3=A_3\backslash A_2\backslash A_1,\cdots,B_n=A_n\backslash A_{n-1}\backslash\cdots\backslash A_1$. It's obvious that by taking the difference of events $\left.\{A\}\right|_{i=1}^n$, events $\left.\{B\}\right|_{i=1}^n$ must be disjoint with each other, because $B_k$ stands for elements which are unique on $A_k$ from $\left.\{A\}\right|_{i=1}^k$. 
	
On the other hand, their union will not be changed, i.e. $\bigcup_{i}A_i=\bigcup_{i}B_i$. That's because for each element in $\bigcup_{i}A_i$, it must be in one of $A_i$, then it must be in one of $B_i$. 
	
Plus a property of probability space that $\Pr(E_1\backslash E_2)=\Pr(E_1)-\Pr(E_1\cap E_2)\leq\Pr(E_1)$, we learn that $\Pr(B_i)\leq\Pr(A_i)$. Therefore, we proved the Union Bound by

$$\Pr(\bigcup_{i=1}^nA_i)=\Pr(\bigcup_{i=1}^nB_i)=\sum_{i=1}^n\Pr(B_i)\leq\sum_{i=1}^nA_i.$$

#### 1-2 Principle of Inclusion and Exclusion

First we need to prove PIE with two events $A$ and $B$. By using some basic property of probability space, we get that
	
$$\Pr(A\cup B)=\Pr(A)+\Pr(B\backslash A)=\Pr(A)+\Pr(B)-\Pr(A\cap B).$$

Then, we can use mathematical induction to prove PIE with $n$ events $A_1,A_2,\cdots,A_n$.
	
Assume that the following equation holds for $n-1$ events,
	
$$\Pr(\bigcup_{i=1}^{n-1}A_i)=\sum_{\emptyset\neq S\in[n-1]}(-1)^{|S|-1}\Pr(\bigcap_{i\in S}A_i).$$
	
By adding the $n$-th event $A_n$, we have
	
$$
\begin{align*}
    \Pr(\bigcup_{i=1}^nA_i)&=\Pr(\bigcup_{i=1}^{n-1}A_i\cup A_n) \\ &=\Pr(\bigcup_{i=1}^{n-1}A_i)+\Pr(A_n)-\Pr(\bigcup_{i=1}^{n-1}A_i\cap A_n) \\ 
    &=\sum_{\emptyset\neq S\in[n-1]}(-1)^{|S|-1}\Pr(\bigcap_{i\in S}A_i)+\Pr(A_n)-\Pr(\bigcup_{i=1}^{n-1}A_i\cap A_n) \\
    &=\sum_{i=1}^n\Pr(A_i)-\sum_{i<j}\Pr(A_i\cap A_j)+\sum_{i<j<k}\Pr(A_i\cap A_j\cap A_k) +\cdots \\
    &=\sum_{\emptyset\neq S\in[n]}(-1)^{|S|-1}\Pr(\bigcap_{i\in S}A_i).
\end{align*}
$$

#### 1-3 Surjection

Recall the definition of a surjective function $f: A\rightarrow B$ is that $f(A)=B$, i.e. $B$ is $A$'s image set. Let $A_i$ be an event that there is no element in $[m]$ which is mapped to $i$. Therefore, the probability of $f: [m]\rightarrow[n]$ to be surjective is
	
$$\Pr(f\text{ is surjective})=\Pr(\bigcap_{i=1}^nA_i^C)=1-\Pr(\bigcup_{i=1}^nA_i),$$

where we uses the De Morgan's laws to address the complement. Then we can use PIE to calculate the last term

$$
\begin{align*}
    \Pr(\bigcup_{i=1}^nA_i)&=\sum_{\emptyset\neq S\in[n]}(-1)^{|S|-1}\Pr(\bigcap{i\in S}A_i) \\ &=\sum_{k=1}^n\sum_{s\in\tbinom{n}{k}}(-1)^{k-1}\Pr(\bigcap_{i\in S}A_i) \\
    &=\sum_{k=1}^n\binom{n}{k}(-1)^{k-1}\left(\frac{n-k}{n}\right)^m.
\end{align*}  
$$  
Although $k=n$ is impossible to happen, we still add such term inside PIE, because the according probability is $0$. Finally we get

$$
\begin{align*}
    \Pr(f\text{ is surjective})&=1-\sum_{k=1}^n\binom{n}{k}(-1)^{k-1}\left(\frac{n-k}{n}\right)^m \\
    &= \sum_{k=1}^n\left(\frac{1}{n}-\binom{n}{k}(-1)^{k-1}\left(\frac{n-k}{n}\right)^m\right) \\
    &= \sum_{k=1}^n\binom{n}{k}(-1)^{n-k}\left(\frac{k}{n}\right)^m.
\end{align*}
$$

#### 1-4 Coprime Integers

Consider arbitrary $x,y\in[n]$ satisfy $\gcd(x,y)=i\in[n]$. Let $\Pr(i)$ be the probability that $\gcd(a,b)=i$. Noticing that $\gcd(a,b)=i$ if and only if $i|a, i|b$ and $\gcd(a/i, b/i)=1$. And we know that the  probability that any natural number is divisible by $n$ is $1/n$. Therefore, we have

$$\Pr(i)=\frac{1}{i}\cdot\frac{1}{i}\cdot\Pr(1)=\frac{\Pr(1)}{i^2}.$$

Obviously, we have $\sum_{i=1}^n\Pr(i)=1$, i.e. $\Pr(1)\cdot\sum_{i=1}^n1/i^2=1$. The probability that $x,y$ are coprime is $\Pr(1) =1/\sum_{i=1}^n1/i^2=1/H_{n,2},$ where $H_{n,2}$ is the generalized harmonic number. It means the number of coprime pairs in $[n]$ is

$$n(n-1)\Pr(1)=\frac{n(n-1)}{H_{n,2}}.$$

**Note**: the generalized harmonic number can be calculated as 

$$H_{n,2}=\frac{1}{2}\sum_{1\leq i,j\leq n}\frac{(i-1)!(j-1)!}{(i+j)!}+\frac{3}{2}\sum_{j=1}^n\frac{1}{k^2\tbinom{2k}{k}}.$$

I think this problem also can be solved using PIE, but I choose a more intuitive version from calculus class. If we want to use PIE to solve the problem, we can let event $A_i$ be randomly choose two integers in $[i]$, then calculate their union, i.e. $\Pr(\bigcup_{i=1}^nA_i)$.

#### 1-5 Bonferroni's inequality and Kounias' inequality

By intuition from Bonferroni's inequality, we have
$$\sum_{\substack{S\subseteq[n] \\ |S|=2k}}(-1)^{|S|-1}\Pr(\bigcap _{i\in S}A_i)\leq\Pr(\bigcup_{i=1}^nA_i)\leq\sum_{\substack{S\subseteq[n] \\ |S|=2k+1}}(-1)^{|S|-1}\Pr(\bigcap _{i\in S}A_i).$$

Therefore, the left-hand-side of Kounia's inequality is just the soft constraint of the Bonferroni's inequality. Because we notice that if $|S_1|<|S_2|$,

$$\left|\sum_{\emptyset\neq S_1\in[n]}(-1)^{|S_1|-1}\Pr(\bigcap_{i\in S_2}A_i)\right|>\left|\sum_{S_2\in[n]}(-1)^{|S_2|-1}\Pr(\bigcap_{i\in S_2}A_i)\right|.$$

For instance, if $|S_1|=2$ and $|S_2|=3$, the above inequality means that

$$\sum_{i<j}\Pr(A_i\cap A_j)>\sum_{i<j<k}\Pr(A_i\cap A_j\cap A_k).$$

Therefore, the left hand side is trivial using PIE and combining each $|S|=2k$ and $|S|=sk+1$ together to scale.

The right hand side can be considered as

$$\Pr(\bigcup_{i=1}^nA_i)=\Pr(A_1\cup\bigcup_{i=2}^n(A_i\backslash A_1))\leq\Pr(A_1)+\sum_{i=2}^n\Pr(A_i\backslash A_1).$$

Since $\Pr(A_i\backslash A_1)=\Pr(A_i)-\Pr(A_i\cap A_1)$, we get the desired right hand side

$$\Pr(\bigcup_{i=1}^nA_i)\leq\sum_{i=1}^n\Pr(A_i)-\sum_{i=2}^n\Pr(A_1\cap A_i).$$

**Note**: Actually, the Kounias' inequality has a slightly stronger conclusion for all $A_i$ not only $A_1$, i.e.

$$\Pr(\bigcup_{i=1}^nA_i)\leq\min_{k\in[n]}\left\{\sum_{i=1}^n\Pr(A_i)-\sum_{i\neq k}\Pr(A_i\cap A_k)\right\}.$$

## Problem 2

![](https://github.com/llllllimitedX/tmpdatas/blob/main/img24/prps102.png?raw=true)

#### 2-1 Symmetric 1D Random Walk (I)

The symmetric 1D random walk can be considered as a recursive process. $A_i$ denotes the event that the gambler earns 0 points after playing $i$ rounds of the game. The conclusion is that

$$\Pr(A_i)=\begin{cases}
    0, &\text{if $i$ is odd,} \\
    \frac{1}{2^i}\binom{i}{i/2}, &\text{if $i$ is even.}
\end{cases}$$

The first case is trivial, because after an odd round of random walks, the amount of money the gambler gets must be odd, it can't be 0. The second case is derived due to the distribution of $i$-th round. In the $i$-th round, the possible values of money that the gamble can obtain range exactly from $-i$ to $i$, including all integers with a identical difference of 2. These coefficients of distribution form binomial coefficients. The intuition is easy to be shown since we choose $k$ HEADs and $i-k$ TAILs, there are totally $\tbinom{i}{k}$ ways to get $2k-i$ amounts of money. And since the binomial distribution is symmetric, it can be maximized when $k=i/2$, i.e. the total amount of money is 0.

Using Stirling's approximation,

$$n!\approx\sqrt{2\pi n}\left(\frac{n}{\text{e}}\right)^n,$$

we can calculate the summation of all probabilities

$$
\begin{align*}
    \sum_{i=1}^\infty\Pr(A_i) &=\sum_{k=1}^\infty\frac{1}{2^{2k}}\binom{2k}{k} 
    =\sum_{k=1}^\infty\frac{1}{2^{2k}}\frac{(2k)!}{(k!)^2} \\
    &\approx\sum_{k=1}^\infty\frac{1}{2^{2k}}\frac{\frac{(2k)^{2k}}{\text{e}^{2k}}\sqrt{2\pi\cdot2k}}{\frac{k^{2k}}{\text{e}^{2k}}2\pi k} 
    =\sum_{k=1}^\infty\frac{1}{\sqrt{\pi k}}=+\infty.
\end{align*}
$$

#### 2-2 Symmetric 1D Random Walk (II)

Following the hint of the problem. 
	
**sp(i)** Consider the definition of events $B_i$(game ends within $i$ rounds) and $C_i$(game ends at the $i$-th round), we find the relationship between $B_i$ and $C_i$, i.e.

$$\Pr(B_i)=\sum_{k=1}^i\Pr(C_k).$$

The complement of $B_i$, i.e. $\bar{B_i}$, means that the gambler will not lose all his $m$ points within $i$ rounds. Plus that $C_1,C_2,\cdots$ are disjoint events, we take complementary of both sides

$$\Pr(\bar{B_i})=1-\sum_{k=1}^i\Pr(C_k)=\sum_{k=i+1}^\infty\Pr(C_k).$$

Therefore, the summation of the probabilities

$$\sum_{i=1}^\infty\Pr(\bar{B_i})=\sum_{i=1}^\infty\sum_{k=i+1}^\infty\Pr(C_k)=\sum_{i=1}^\infty(i-1)\Pr(C_i),$$

since the number $C_i$ occurs is exactly $i-1$ for all $k<i$.

**sp(ii)** Following the hint, we first introduce \textbf{the Ballot Problem}. Suppose that in an election, candidate $A$ receives $a$ votes and candidate $B$ receives $b$ votes, where $a\geq kb$ for some positive integer $k$. Compute the number of ways the ballots can be ordered so that $A$ maintains more than $k$ times as many vote as $B$ throughout the counting of the ballots. \textbf{The Ballot Theorem} tells us that the solution is given by (referenced to Marc Renault, [Four_Proofs_of_the_Ballot_Theorem](https://www-users.cse.umn.edu/~reiner/Classes/Four_Proofs_of_Ballot_Theorem.pdf))

$$\frac{a-kb}{a+b}\binom{a+b}{a}.$$

In this problem, $a$ and $b$ denote for number of TAILs and HEADs within $i$-th round. And $k=1$ because we only need to guarantee that $a>b$ to get the failure. More specifically, $a+b=i$ because we exactly lose the game at the $i$-th round, $a-b=m$ because we have originally $m$ points. Therefore, number of ways to lose the game at the $i$-th round is

$$\frac{a-b}{a+b}\binom{a+b}{a}=\frac{m}{i}\binom{i}{(i+m)/2}.$$

Plus that the total number of permutations within $i$ rounds is $2^i$, the probability that the gambler loses the game at the $i$-th round is

$$\Pr(C_i)=\frac{m}{i\cdot2^i}\binom{i}{(i+m)/2}=\frac{m\cdot i!}{2^i\cdot i}\left(\left(\frac{i+m}{2}\right)!\left(\frac{i-m}{2}\right)!\right)^{-1}.$$

Notice that here the combinatorial number and the factorial number is generalized, which means we only use the definition formula. And if $i<m$, then $((i-m)/2)!=0!=1.$

**sp(iii)** Using Stirling's formula to approximate $\Pr(C_i)$, and substituting it to $\Pr(\bar{B}_i)$, we can get that

$$
\begin{align*}
    \sum_{i=1}^\infty \Pr(\bar{B}_i)&=\sum_{i=1}^\infty\frac{m\cdot i!\cdot(i-1)}{2^i\cdot i}\left(\left(\frac{i+m}{2}\right)!\left(\frac{i-m}{2}\right)!\right)^{-1}\\&\approx\sum_{i=1}^\infty \frac{m}{\sqrt{2\pi}}\left(\frac{i}{2}\right)^i\rightarrow+\infty.
\end{align*}
$$

## Problem 3

![](https://github.com/llllllimitedX/tmpdatas/blob/main/img24/prps103.png?raw=true)

#### 3-1 Noexistence of Probability Space

First, we need to prove that it is impossible to define a uniform probability law on the set of natural numbers $\mathbb{N}$.
	
Assume that there exist a probability space $(\mathbb{N}, 2^\mathbb{N}, \Pr)$ such that $\Pr(\{i\})=\Pr(\{j\})$ for all $i,j\in \mathbb{N}$. Consider the total probability of the entire sample space $\mathbb{N}$: $\Pr(\mathbb{N})=\Pr(\{1\})+\Pr(\{2\})+\cdots$. Since each singleton set has the same probability, let's denote this common probability as $p$. Give n that $\Pr(\mathbb{N})=1$ (as it is a probability measure over the entire sample space), we have $1=p+p+\cdots=\infty\cdot p$. This equation implies that $p=0$, because otherwise the sum would diverge. However, this means that the probability of every singleton set in $\mathbb{N}$ is zero. Yet, by the countable additivity property of probability measures, we know that $\sum_{i}\Pr(\{i\})=\sum_i0=0$, which contradicts to the one-summation rule. Therefore, our assumption that a uniform probability law exists on $\mathbb{N}$ must be false.

For the second statement, proving that there is no uniform probability law on the real interval $[0,1]$, the same argument cannot be used because the real interval $[0,1]$ is uncountably infinite, whereas the set of natural numbers $\mathbb{N}$ is countably infinite.

We have used an important property from mathematical analysis. It states that the sum of a countable number of zeros is always zero, while the sum of an infinite uncountable number of zeros is indeterminate. In fact, for the real interval [0,1], probability (measure) can be defined using geometric probability models, which implies that $\Pr(\left(l,r\right])=r-l$ for any intervals $\left(l,r\right]\subseteq[0,1]$.

#### 3-2 Smallest $\sigma$-Field

Let $\mathcal{F}_\alpha$, where $\alpha$ is an index set, be a collection of $\sigma-$fields containing $S$. First, We need to prove $\mathcal{F}=\bigcap_\alpha\mathcal{F}_\alpha$ is itself a $\sigma$-field.

- Empty set. Trivially, since for all $\alpha$,  $\mathcal{F}_\alpha$ contains empty set. 
- Closure under complement. Let $A\in\mathcal{F}$, then $A\in\mathcal{F}_\alpha$ for all $\alpha$. Since each $\mathcal{F}_\alpha$ is a $\sigma$-field, $A^C\in\mathcal{F}_\alpha$ for all $\alpha$. Thus, $A^C\in\mathcal{F}$.
- Closure under countable union. Let $A_1, A_2, \ldots \in \mathcal{F}$. Then, $A_i \in \mathcal{F}_\alpha$ for all $\alpha$. Since each $\mathcal{F}_\alpha$ is a $\sigma$-field, $\bigcup_{i} A_i \in \mathcal{F}_\alpha$ for all $\alpha$. Thus, $\bigcup_{i} A_i \in \mathcal{F}$.

These three basic rules determine that $\mathcal{F}$ is a $\sigma$-field. Second, we need to prove that $\mathcal{F}$ is the smallest $\sigma$-field containing $S$. Let $\mathcal{G}$ be any $\sigma$-field containing $S$, i.e. $S\subseteq\mathcal{G}$. Since $\mathcal{F}$ is defined as the intersection of all such $\sigma$-fields containing $S$, it follows that $\mathcal{F}\subseteq\mathcal{G}$, which means that $\mathcal{F}$ is the smallest $\sigma$-field containing $S$.

Therefore, we have shown both parts, and hence proved that the smallest $\sigma$-field containing $S$ is given by $\mathcal{F}$, i.e. the intersection of all $\sigma$-fields containing $S$.

#### 3-3 Union of $\sigma$-Field

The union of two $\sigma$-fields is not necessarily a $\sigma$-field. Intuitively, let two subsets $A,B\subseteq\Omega$, the according smallest $\sigma-$fields are $\mathcal{F}=\{\emptyset, \Omega, A, A^C\}$ and $\mathcal{G}=\{\emptyset, \Omega, B, B^C\}$. However, their union $\mathcal{F}\cup\mathcal{G}=\{\emptyset, \Omega, A, B, A^C, B^C\}$ is NOT a $\sigma$-field because the closure under countable union does not hold any more. For instance, $A\cup B\notin\mathcal{F}\cup\mathcal{G}$ for any time.

#### 3-4 Probability Space?

$(\Omega,\mathcal{F},\Pr)$ is a probability space. Here's the proof. First, we need to show that $(\Omega, \mathcal{F})$ is a $\sigma$-field.
	
Denote that $\mathcal{F}=\mathcal{F}_1\cup\mathcal{F}_2$, where $\mathcal{F}_1=\{A\in\Omega | A \text{ is countable}\}$ and $\mathcal{F}_2=\{A\in\Omega | A^C \text{ is countable}\}$.

- Empty set. Trivially, since $\emptyset\in\mathcal{F}_1\subseteq\mathcal{F}$.
- Closure under complement. For countable set $A\in\Omega$, we have $A\in\mathcal{F}_1$, its complement $A^C\in\mathcal{F}_2$. For countable set $B^C\in\Omega$, we have $B^C\in\mathcal{F}_1$, its complement $(B^C)^C=B\in\mathcal{F}_2$. 
- Closure under countable union. Suppose that $A_1, A_2,\cdots$ is a sequence of sets in $\mathcal{F}$. If for all $i\in\mathbb{N}^*$, $A_i\in\mathcal{F}_1$, then $\bigcup_{i}A_i$ is countable union of countable sets, thus countable, so $\bigcup_iA_i\in\mathcal{F}_1\subseteq\mathcal{F}$. Otherwise, these exist $i_0\in\mathbb{N}^*$ such that $A_{i_0}\in\mathcal{F}_2$, thus $(\bigcup_iA_i)^C\subseteq A_{i_0}^C$ is a subset of a countable set, thus countable, so $\bigcup_iA_i\in\mathcal{F}_2\subseteq\mathcal{F}$.
  
We managed to prove that $(\Omega, \mathcal{F})$ is a $\sigma$-field. Then we should to deal with $\Pr$. Notice that $\mathcal{F}_1\cap\mathcal{F}_2=\emptyset$, which guarantee that $\Pr$ is well-defined. In fact, since $\Omega=\mathbb{R}$ is not countable(whose cardinality is $\aleph$), for any $A\in\mathcal{F}_1\cap\mathcal{F}_2$, we have that $\Omega=A\cup A^C$ is countable, leads to a contradiction.
    
Suppose that $A_1,A_2,\cdots$ is a sequence of disjoint sets in $\mathcal{F}$. If for all $i\in\mathbb{N}^*$, $A_i\in\mathcal{F}_1$, as we proved $\bigcup_iA_i\in\mathcal{F}_1$, thus $\Pr(\bigcup_iA_i)=0=\sum_i0=\sum_i\Pr(A_i)$. Otherwise, suppose that $i_0\in\mathbb{N}^*$ satisfies that $A_{i_0}\in\mathcal{F}_2$, then for any $i\neq i_0*$, suppose that $A_i\in\mathcal{F_2}$, since $A_i\cap A_{i_0}=\emptyset$, we have $\Omega=\emptyset^C=(A_i\cap A_{i_0})^C=A_i^C\cup A_{i_0}^C$ is an union of two countable sets, thus countable, leads to a contradiction. Therefore $A_i\in\mathcal{F}_1$ for $i\neq i_0$. As proved previously, $\bigcup_iA_i\in\mathcal{F}_2$. Therefore, we have

$$\Pr(\bigcup_iA_i)=1=1+0=1+\sum_{i\neq i_0}0=\Pr(A_{i_0})+\sum_{i\neq i_0}\Pr(A_i)=\sum_i\Pr(A_i).$$

Plus, trivially we have $\Pr(\Omega)=1$, because $\Omega=\mathbb{R}$ is uncountable. Finally we proved that $(\Omega, \mathcal{F}, \Pr)$ is exactly a probability space.

#### 3-5 $\sigma$-Field?

Let $A$ be the set of even numbers. Then $A\in\mathcal{A}$ with $\theta=1/2$/ Let $I_0=\{1\},I_k=\{n|2^{k-1}<n\leq2^k\}$, for $k=1,2,\cdots$. Construct $B$ as follows:

$$B=\bigcup_{k=0}^\infty\{(I_{2k}\cap A^C)\cup(I_{2k+1}\cap A)\}.$$

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

## Problem 4

![](https://github.com/llllllimitedX/tmpdatas/blob/main/img24/prps104.png?raw=true)

#### 4-1 Positive Correlation

1. Due to the Bayes' Law, we have

$$\Pr(B|A)=\frac{\Pr(A|B)\cdot\Pr(B)}{\Pr(A)}>\Pr(B),$$

which means $A$ gives positive information about $B$ too.

2. Due to chain rule, the fact that $B$ gives positive information about $A$ tells us that $\Pr(A\cap B)>\Pr(A)\Pr(B)$. Therefore, using the definition of conditional probability, we have
	
$$\Pr(A|\bar{B})=\frac{\Pr(A\cap\bar{B})}{\Pr({\bar{B}})}=\frac{\Pr(A)-\Pr(A\cap B)}{1-\Pr(B)}<\frac{\Pr(A)(1-\Pr(B))}{1-\Pr(B)}=\Pr(A),$$
	
which means $\bar{B}$ gives negative information about $A$.

3. We need to consider the relationship between $\Pr(\bar{A}|\bar{B})$ and $\Pr(\bar{A})$. Using De Morgan's law to convert the complement, we have

$$\Pr(\bar{A}|\bar{B})=\frac{\Pr(\bar{A}\cap\bar{B})}{\Pr(\bar{B})}=\frac{\Pr(\overline{A\cup B})}{1-\Pr(B)}=\frac{1-\Pr(A\cup B)}{1-\Pr(B)}.$$

Using the principle of inclusion and exclusion, we have

$$
\begin{align*}
\Pr(\bar{A}|\bar{B})
&=\frac{1-\Pr(A)-\Pr(B)+\Pr(A\cap B)}{1-\Pr(B)}\\
&>\frac{1-\Pr(A)-\Pr(B)+\Pr(A)\Pr(B)}{1-\Pr(B)}\\
&=\frac{(1-\Pr(A)(1-\Pr(B)))}{1-\Pr(B)} \\
&=1-\Pr(A)=\Pr(\bar{A}),
\end{align*}
$$

which means that $\bar{B}$ gives positive information about $\bar{A}$.

#### 4-2 Balls in Urns (I)

1. Let event $A$ be that the first ball is black, event $B$ be that the second ball is black. Because we pick an urn uniformly, the probability that each urn is chosen is $1/n$. Therefore,

$$\Pr(A)=\frac{1}{n}\left(\frac{n-1}{n-1}+\frac{n-2}{n-1}+\cdots+\frac{1}{n-1}+\frac{0}{n-1}\right)=\frac{1}{2}.$$

An intuition is that white and black are symmetry here. Therefore, when we pick out two balls, the probability that the two balls have same color(black/black or white/white) is same, which means $\Pr(A\cap B)=\Pr(\overline{A\cup B})$. 

At the same time, due to the principle of inclusion and exclusion, we have $\Pr(\overline{A\cup B})=1-\Pr(A\cup B)=1-\Pr(A)-\Pr(B)+\Pr(A\cap B)$. Therefore, $\Pr(A)+\Pr(B)=1$, leading the result

$$\Pr(\text{the second ball is black})=\Pr(B)=1-\Pr(A)=\frac{1}{2}.$$

The intuition is simple: if we don't care the color of the first ball, then the second ball's color still holds symmetry.

2. We need to calculate the probability that two balls are both black.

$$\Pr(A\cap B)=\frac{1}{n}\sum_{i=1}^{n}\frac{(i-1)(i-2)}{(n-1)(n-2)}=\frac{1}{3}.$$

Therefore, the probability that the second ball is black, given that the first is black, i.e. $\Pr(B|A)$ can be calculated as

$$\Pr(B|A)=\frac{\Pr(A\cap B)}{\Pr(A)}=\frac{2}{3}.$$

This can be counter-intuitive. When it is clear that the number of black and white balls is the same, in the case of the first black ball, the probability of the second black ball is 2/3. This is because the distribution of balls in different urns is not uniform, but more "extreme".

#### 4-3 Balls in Urns (II)

1. The first white ball drawn is the $(k+1)$-th ball, which means the first $k$ balls are all black. Therefore, the probability is given by

$$\Pr(\text{the first white ball is $(k+1)$-th ball})=\begin{cases}
    0, &\text{if }k>b, \\
    \frac{w}{w+b-k}\prod_{i=0}^{k-1}\frac{b-i}{w+b-i}, &\text{if }k\leq b.
\end{cases}$$ 

2. An intuition is that in a urn, the probability that the last ball drawn is a white ball is equal to the probability that the first ball drawn is a white ball. It can be proved using Chain Rule to eliminate telescopic terms. It can also be analyzed by considering the inverse of the process, which is identical because the process is just uniform and random. Therefore, the probability is given by

$$\Pr(\text{the last ball is white})=\frac{w}{w+b}.$$

#### 4-4 Noisy Channel

It's a classical conditional probability problem, just like the Dominating False Positive problem introduced in the lecture. Let event $A$ be a true dot(which means it is indeed a dot), event $B$ be a positive dot(which means we receive a dot). Due to Bayes' Law, the probability is given by

$$\Pr(A|B)=\frac{\Pr(A)\cdot\Pr(B|A)}{\Pr(B)}=\frac{\frac{3}{7}\cdot\frac{7}{8}}{\frac{3}{7}\cdot\frac{7}{8}+\frac{4}{7}\cdot\frac{1}{8}}=\frac{21}{25}.$$

## Problem 5

![](https://github.com/llllllimitedX/tmpdatas/blob/main/img24/prps105.png?raw=true)

#### 5-1 Limited Independence

Consider a simple case where $n=2$ and $p=1/2$, which can be regarded as flipping a fair coin twice. Define events $A,B$ and $C$ as following:
- Event $A$: the first drop is HEAD with $\Pr(A)=1/2$;
- Event $B$: the second drop is HEAD with $\Pr(B)=1/2$;
- Event $C$: the two drops get the same result with $\Pr(C)=1/2$.

These three events are pairwise independent, because 

$$\Pr(A\cap B)=\Pr(A)\Pr(B)=1/4,$$ 

$$\Pr(A\cap C)=\Pr(A)\Pr(C)=1/4,$$ 

$$\Pr(B\cap C)=\Pr(B)\Pr(C)=1/4.$$ 

But $A,B$ and $C$ are not mutually independent, because

$$\Pr(A\cap B\cap C)=1/4,$$

$$\Pr(A)\Pr(B)\Pr(C)=1/8.$$

For general $n$ and $p$ case, I am still bewildering... If you have any great ideas, please contact me with my email. **(TBD)**

#### 5-2 Product Distribution

1. The optimization problem tells us to find the optimal $\hat{p}$ to maximize the probability that $k$ out of $n$ Bernoulli trials with prob. $\hat{p}$ succeed. It is given by Binomial probability, i.e.

$$\Pr(\text{$k$ out of $n$ trials succeed})=\binom{n}{k}\hat{p}^k(1-\hat{p})^{n-k}.$$

Notice that $\tbinom{n}{k}$ is just coefficient, out optimization objective should be $\hat{p}^k(1-\hat{p})^{n-k}$. Therefore, take monotonically increasing logarithms

$$\ln(\hat{p}^k(1-\hat{p})^{n-k})=k\ln\hat{p}+(n-k)\ln(1-\hat{p}).$$

Set the derivative to be zero, we get out optimal solution

$$\frac{k}{\hat{p}}-\frac{n-k}{1-\hat{p}}=0\Rightarrow\hat{p}=\frac{k}{n},$$

which is just the proportion of succeeded trials. Quite intuitive!

2. If someone tells you exactly which $k$ trials succeeded, it will not help us estimate $p$ more accurately. This is because we are conducting a series of n independent Bernoulli trials, each with an equal probability and no relationship between them. Therefore, it doesn't matter which specific trial was successful; what matters is the number of successful trials, $k$.

## Problem 6

![](https://github.com/llllllimitedX/tmpdatas/blob/main/img24/prps106.png?raw=true)

#### 6-1 Satisfiability (I)

A trivial case would be $k>n$, which means each clause would have more than $n$ literals. In that case, every clause will be satisfiable because there must be $x_i$ such that both $x_i$ and its negation $\bar{x}_i$ occurs in that clause, making it satisfiable for disjunction. Therefore if $k>n$, $\Phi$ would be satisfiable at all. The following discussion will be within $k\leq n$.
	
We can randomly choose a truth assignment $x=(x_1,x_2,\cdots,x_n)$. Define a random event $A$: $\Phi(x)=1$. Easily to see that $A$ is true if and only if all its clauses are true. Therefore, define the random events $A_i$: clause $C_i$ is satisfiable, $i\in[m]$. 

Since each clause contains $k$ literals, and $k\leq n$, the probability that $C_i$ is false is $1/2^k$, i.e. $\Pr(\overline{A_i})=1/2^k$. Therefore, take the junctions, we get (by using De Morgan's law and Union Bound):

$$
\begin{align*}
    \Pr(A) &= \Pr(A_1\wedge A_2\wedge\cdots\wedge A_m) \\
    &=1-\Pr(\overline{A_1}\vee\overline{A_2}\vee\cdots\vee\overline{A_n}) \\
    &\geq 1-\sum_{i=1}^m\Pr(\overline{A_i}) \\
    &=1-\frac{m}{2^k}>0.
\end{align*}
$$

Due to the probabilistic method, we learn that $\Phi(x)$ should be satisfiable since the probability that $\Phi(x)=1$ is greater than zero, which means there must exist a truth assignment to satisfy a particular $k$-CNF.

#### 6-2 Satisfiability (II)

To prove that a $k$-CNF problem is satisfiable when the number of clauses $m<2^k$, we can construct a feasible solution by following way.
	
Firstly, we set all variables \(x_1, \cdots, x_n\) to true. Consequently, all clauses containing the original variables \(x_i\) (not negations \(\bar{x_i}\)) are satisfied.

Next, we consider the clauses composed entirely of negations. Sorting them in ascending order based on index, we flip the value of the variable corresponding to the smallest index in each clause (setting it to false), ensuring satisfiability for these clauses.

At this point, some clauses initially set to true might become unsatisfiable due to the flipping of certain variable values. Let's refer to these variables as "pivot variables" and refrain from altering their values. For the unsatisfied clauses, also sorted in ascending order, we flip the value of the variable corresponding to the smallest index among the non-"pivot variables", ensuring satisfiability for these clauses.

We repeat this process until all clauses are satisfiable. This is achievable because we've emphasized in (I) that \(k \leq n\) (otherwise trivial), indicating that the number of variables \(k\) in each clause is at most the total number of variables \(n\). Therefore, we iterate the above steps at most \(k\) times. As a variable can be flipped at most \(k\) times, this ensures that in the worst-case scenario, all \(n\) variables are flipped, resulting in the satisfaction of each clause. A more intuitive and straightforward explanation is that $k\leq n$ means that there must exists a true-value literal in every clause. 

#### 6-3 Satisfiability (III)

If $m\geq2^k$, $\lfloor m(1-1/2^k)\rfloor\geq2^k(1-1/2^k)=2^k-1$, which means that there will be at least $2^k-1$ clauses be satisfiable. It is consistent with our intuition from (I) since we know that $\Phi$ is always satisfiable for less than $2^k$ clauses. 
	
Let $T_j$ be a random variable defined as follows: if clause $j$ is satisfied by the assignment, then $T_j = 1$, otherwise $T_j = 0$. From (I), we can easily know that $\Pr(T_j=0)=1/2^k$. Therefore, the expectation of $T_j$ should be

$$\mathbb{E}[T_j]=\Pr(T_j=1)=1-\frac{1}{2^j}.$$

Therefore, let $T$ be the random variable denoting the total number of satisfied clauses, we have $T=\sum_{i=1}^mT_i$. By linearly of expectation, we have

$$\mathbb{E}[T]=\sum_{i=1}^m\mathbb{E}[T_m]=m\left(1-\frac{1}{2^k}\right).$$

Using Markov's inequality, we have

$$\Pr\left(T\geq\lfloor m\left(1-\frac{1}{2^k}\right)\rfloor\right)\geq1-\frac{\mathbb{E}[T]}{\lfloor m\left(1-\frac{1}{2^k}\right)\rfloor}>0.$$

By probability method, we learn that there must exists a truth assignment satisfying at least $\lfloor m(1-1/2^k)\rfloor$ clauses in $\Phi$. End of proof.