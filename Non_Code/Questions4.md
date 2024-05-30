## Property of Poisson process
Q: You are waiting for a bus at a bus station. The buses arrive at the station according to a Poisson process with an average arrival time of 10 minutes ($\lambda$ = 0.1/min). If the buses have been running for a long time and you arrive at the bus station at a random time, what is your expected waiting time? On average, how many minutes ago did the last bus leave?

A: both $\frac{1}{\lambda}$

## Moments of normal distribution
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

## Connecting noodles
You have 100 noodles in your soup bowl. Being blindfolded, you are told to take two ends of some noodles (each end on any noodle has the same probability of being chosen) in your bowl and connect them. You continue until there are no free ends. The number of loops formed by the noodles this way is stochastic. Calculate the expected number of circles.
