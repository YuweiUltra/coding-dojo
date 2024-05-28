## Birthday line
Q：At a movie theater, a whimsical manager announces that she will give a free ticket to the first person in line whose birthday is the same as someone who has already bought a ticket. You are given the opportunity to choose any position in line. Assuming that you don't know anyone else's birthday and all birthdays are distributed randomly throughout
the year (assuming 365 days in ayear), what position in line gives you the largest chance of getting the free ticket?

A：Assume there are n people ahead in the line. 
We need to know the probability of all n people with none of two have the same birthday date.
We also need to know the probability that we have the same birthday date with one previous people in the line.

$$P(\text{all } D_i \ne D_j \text{ for every } i,j) = \frac{{365 \choose n} \times n!}{365^n}$$

$$P( \text{there exist i in \{1,2,...n\} } D_i=D_{n+1})=\frac{n}{365}$$

## Dice order
Q: We throw 3 dice one by one. What is the probability that we obtain 3 points in strictly increasing order?

A: 
$$P(x_1\ne x_2 \ne x_3)=\frac{{6 \choose 3}\times 3!}{6^3}$$
Answer is $\frac{1}{6}\times P(x_1\ne x_2 \ne x_3)$

## Amoeba population
Q: There is a one amoeba in a pond. After every minute the amoeba may die, stay the same, split into two or split into three with equal probability. All its offspring, if it has any, will behave the same (and independent of other amoebas. What is the probability the amoeba population will die out?

A: Let M(x) denote the probability that the population will die out with current population is x.
$$M(1)=\frac{1}{4}\times (1+M(1)+M(2)+M(3))$$
$M(2)=M(1)^2, M(3)=M(1)^3$

## Candies in a jar
Q: You are taking out candies one by one from ajar that has 10 red candies, 20 blue candies, and 30green candies in it. What is the probability that there are at least 1 blue candy and 1 green candy left in the jar when you have taken out all the red candies

A: 

$$
\begin{aligned}
    P(\text{red out last}) &= \frac{1}{6}, \\
    P(\text{blue out last}) &= \frac{2}{6}, \\
    P(\text{green out last}) &= \frac{3}{6}
\end{aligned}
$$

$$
\begin{aligned}
    &P(\text{green out last}) \times P(\text{blue out last | green out last}) + P(\text{blue out last}) \times P(\text{green out last | blue out last}) \\
    &= \frac{3}{6} \times \frac{2}{3} + \frac{2}{6} \times \frac{3}{4} \\
    &= \frac{1}{3} + \frac{1}{4}=\frac{7}{12}
\end{aligned}
$$

## Russian roulette series

## Aces
Q: Fifty-two cards are randomly distributed to 4 players with each player getting 13 cards. What is the probability that each of them will have an ace?

A: $$\frac{13^4}{{52 \choose 4}}$$

## Gambler's ruin problem

Q: $$P_0=0, P_N=1, P_i=pP_{i+1}+qP_{i-1}$$
