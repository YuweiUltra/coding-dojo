## Property of Poisson process
Q: You are waiting for a bus at a bus station. The buses arrive at the station according to a Poisson process with an average arrival time of 10 minutes ($\lambda$ = 0.1/min). If the buses have been running for a long time and you arrive at the bus station at a random time, what is your expected waiting time? On average, how many minutes ago did the last bus leave?

A: both $\frac{1}{\lambda}$

## `Moments of normal distribution`
Q: If X follows standard normal distribution (X ~ N(0, 1)), what is $E[X^{n}]$ for n= 1, 2, 3 and 4

A: 

$$\begin{align*}
M(t) &= E[e^{tx}] = \int_{-\infty}^{\infty} e^{tx} f(x)  dx \\
M'(t) &= E[xe^{tx}], M'(0) = E[x], M''(0) = E[x^2] \\
\\
M(t) &= \int_{-\infty}^{\infty} e^{tx} \times \frac{1}{\sqrt{2\pi}} \times e^{\frac{-x^2}{2}}  dx \\
&= \frac{1}{\sqrt{2\pi}} \times \int_{-\infty}^{\infty} e^{\frac{-x^2}{2} + tx}  dx \\
&= e^{\frac{1}{2}t^2} \times \int_{-\infty}^{\infty} \frac{1}{\sqrt{2\pi}} \times e^{\frac{-1}{2}(x-t)^2}  dx \\
\end{align*}$$

$$\begin{align*}
\int_{-\infty}^{\infty} \frac{1}{\sqrt{2\pi}} \times e^{\frac{-1}{2}(x-t)^2}  dx \text{ is the pdf of normal distribution } X \sim N(0, 1), \text{ so } \int f(x)  dx = 1
\end{align*}$$

$$\begin{align*}
M(t) &= e^{\frac{1}{2}t^2}
\end{align*}$$

## `Connecting noodles`
Q: You have 100 noodles in your soup bowl. Being blindfolded, you are told to take two ends of some noodles (each end on any noodle has the same probability of being chosen) in your bowl and connect them. You continue until there are no free ends. The number of loops formed by the noodles this way is stochastic. Calculate the expected number of circles.

A:
$$E[f(n)]=\frac{n}{{2n \choose 2}}(E[f(n-1)]+1)+(1-\frac{n}{{2n \choose 2}})E[f(n-1)]=E[f(n-1)]+\frac{n}{{2n \choose 2}}$$

## Optimal hedge ratio
Q: You just bought one share of stock A and want to hedge it by shorting stock B. How
many shares of B should you short to minimize the variance of the hedged position? Assume that the variance of stock A's return $\sigma_A^2$; the variance of B's return is $\sigma_B^2$;
their correlation coefficient is $\rho$.

A: 
$$\Delta = \frac{\rho \sigma_A}{\sigma_B}$$

## `Card game`
A: What is the expected number of cards that need to be turned over in a regular 52-card deck in order to see the first ace?

Q: $X_i$ is 1 if card i is turned over before 4 Aces. 
$$X=1+\sum_{i=1}^{48} X_i$$
$$E[X_i]=\frac{1}{5}$$
$$\text{each card i is equally likely to be in one of the five regions separated by 4 aces}$$

## `Sum of random variables`
Assume that $X_1, X_2 ,.., and X_n$ are independent and identically-distributed (IID) random variables with uniformdistribution between 0 and 1. What is the probability that $S_n= X_1 +X_2 +...+x_n \leq 1$?

Q: $\frac{1}{n!}$

## `Coupon collection`
Q: There are N distinct types of coupons in cereal boxes and each type, independent of prior selections, is equally likely to be in a box.\
A. If a child wants to collect a complete set of coupons with at least one of each type, how many coupons (boxes) on average are needed to make such a complete set?\
B. If the child has collected n coupons, what is the expected number of distinct coupon types?

A:
(A) let $X_i$ be the number of additional coupons needed to ontain the i-th type after (i-1) distinvt types have been collected.
$$X=X_1+X_2+...+X_N=\sum_{i=1}^{N}X_i$$
$$E[X_i]=\frac{N}{N-i+1}$$

(B) let $I_i$ be the indicator if at least one coupon of the i-th type is collected in the set of n coupons
$$Y=I_1+I_2+...+I_N$$
$$E[I_i]=1-(\frac{N-1}{N})^n$$

## `Joint default probability`
Q: If there is a 50% probability that bond A will default next year and a 30% probability that bond B will default.
What is the range of probability that at least one bond defaults and what is the range of their correlation?

A: 
[0.5,0.8]

$$P(\text{A or B defaults})=E[I_A]+E[I_B]-E[I_AI_B]=E[I_A]+E[I_B]-(E[I_A]E[I_B]-cov(I_A,I_B))=0.65-\sqrt{0.21}/2\rho_{AB}$$
$$\tho_{AB}=[-sqrt{3/7},sqrt{3/7}]$$

