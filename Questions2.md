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

A: Caculate the combination in specific cases and divided by total combination ${52 \choose 5} = \frac{52!}{5!(52-k)!}$
- four-of-a-kind: ${13 \choose 1}{4 \choose 4}{12 \choose 1}{4 \choose 1}$
- full house: ${13 \choose 1}{4 \choose 3}{12 \choose 1}{4 \choose 2}$
- two pairs: ${13 \choose 2}{4 \choose 2}{4 \choose 2}{11 \choose 1}{4 \choose 1}$

## Hopping rabbit
Q: A rabbit sits at the bottom of a staircase with n stairs. The rabbit can hop up only one or two stairs at a time. How many different ways are there for the rabbit to ascend to the top of the stairs?

A: let f(n) be the number of ways to climb on n stairs. So, $f(n)=f(n-1)+f(n-2)$ and $f(1)=1$ and $f(2)=2$

## Screwy pirates 2
Q: Having peacefully divided the loot (in chapter 2), the pirate team goes on for more looting and expands the group to 11 pirates. To protect their hard-won treasure, they gather together to put all the loot in a safe. Still being a democratic bunch, they decide that only a majority - any majority - of them (≥6) together can open the safe. So they ask a locksmith to put a certain number of locks on the safe. To access the treasure, every lock needs to be opened. Each lock can have multiple keys; but each key only opens one lock. The locksmith can give more than one key to each pirate.
What is the smallest number of locks needed? And how many keys must each pirate carry??

A: clocks ${11 \choose 5}$. 6 keys for every clock. $\frac{{11 \choose 5} \times 6}{11}$

## Chess tournament
Q: A chess tournament has $2^n$ players with skills 1 > 2 >. . . >$2^n$. It is organized as a knockout tournament, so that after each round only the winner proceeds to the next round. Except for the final, opponents in each round are drawn at random. Let's also assume that when two players meet in a game, the player with better skills always wins. What's the probability that players 1and 2 will meet in the final?

Q: $\frac{2^{n-1}}{2^n-1}$

## Application letters
Q: You're sending job applications ot 5 firms: Morgan Stanley, Lehman Brothers, UBS, Goldman Sachs, and Merrill Lynch. You have 5envelopes on the table neatly typed with names and addresses of people at these 5 firms. You even have 5 cover letters personalized to each of these firms. Your 3-year-old tried to be helpful and stuffed each cover letter into each of the envelopes for you. Unfortunately she randomly put letters into envelopes without realizing that the letters are personalized. 
What is the probability that al 5cover letters are mailed to the wrong firms?"

A: $\frac{11}{30}$

## 100th digit
Q: What is the 100th digit to the right of the decimal point in the decimal representation of $(1 +\sqrt{2})^{3000}$#

A: 9
