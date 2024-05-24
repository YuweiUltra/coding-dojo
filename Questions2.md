## Coin toss game
Q: Two gamblers are playing a coin toss game. Gambler A has (n +1) fair coins; B has n
fair coins. What is the probability that A will have more heads than B if both flip all their coins\
A: Let H(n) be the number of heads in n flips.

$$
\begin{aligned}
&P(H_{A}(n) < H_{B}(n)) = P(H_{A}(n) > H_{B}(n)) \\
&P(H_{A}(n) < H_{B}(n)) + P(H_{A}(n) > H_{B}(n)) + P(H_{A}(n) = H_{B}(n)) = 1 \\
&P(H_{A}(n+1) > H_{B}(n)) = \frac{1}{2} \times P(H_{A}(n) = H_{B}(n)) + P(H_{A}(n) > H_{B}(n)) = \frac{1}{2}
\end{aligned}
$$

## Card game
Q: A casino offers a simple card game. There are 52 cards in a deck with 4 cards for each jack queen king ace
value 2, 3, 4, 5, 6, 7, 8, 9, 10, J, Q, K, A. Each time the cards are thoroughly shuffled (so each card has equal probability of being selected). You pick up a card from the deck and the dealer picks another one without replacement. If you have a larger number, you win; if the numbers are equal or yours is smaller, the house wins as in all other casinos, the house always has better odds of winning. What is your probability of winning?

A: $(1-\frac{3}{51}) \times \frac{1}{2}=\frac{24}{51}=\frac{8}{17}$

## Drunk passenger
Q: A line of 100 airline passengers are waiting to board a plane. They each hold a ticket to one of the 100 seats on that flight. For convenience, let's say that the n-th passenger in line has a ticket for the seat number n. Being drunk, the first person in line picks a random seat (equally likely for each seat). All of the other passengers are sober, and will go to their proper seats unless it is already occupied; In that case, they will randomly choose a free seat. You're person number 100. What is the probability that you end up in your seat (i.e., seat #100) 

A: If the drunk passenger takes the seat #1, then you will end up in your seat #100. If the drunk passenger takes the seat #100, then
you will not end up in your seat. 

If the drunk passenger takes seat #N from #2 to #99, then the #N passenger will be the new drunk passenger with the same probability of chossing #1 or #100 seat.
So the probability of ending up in seat #100 is equal to not ending up in seat #100, which is  $\frac{1}{2}$.

## N points on a circle
Q: Given N points drawn randomly on the circumference of a circle, what is the probability that they are all within a semicircle

A: Select one point from N points and define a semicircle with its first or left radius passes the selected point. The other n-1 points have $2^{-(N-1)}$ probability to fall into the semicircle. So the answer is $N \times 2^{-(N-1)}$ 

## Pokerhands
Q: What are the probabilities of getting hands with four-of-a-kind (four of the five cards with the same value? Hands with a full house (three cards of one value and two cards of another value)? Hands with two pairs?

A: Caculate the combination in specific cases and divided by total combination $$
- four-of-a-kind:
$${52 \choose 5} = \frac{52!}{5!(52-k)!}$$



