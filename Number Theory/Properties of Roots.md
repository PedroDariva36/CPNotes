#Number_Theory

When we start our journey into number theory, we must learn a few general rules and identities, A good portion of those identities involve roots, in this section we will list a few.

### Divisors, Prime Factorization

It can be proven that for any integer $N$, it can be expressed as a multiplication of 2 numbers, $p$ and $q$:

$$p \cdot q = N$$

Now, for the sake of contradiction, let's say that both $q$ and $p$ are in fact prime numbers, and not only that, but both of them must be greater than the square root of $N$:
$$
\begin{aligned}
q > \sqrt{N} \\ p > \sqrt{N}
\end{aligned}
$$

Now, can $q \cdot p$ still be equal to $N$?
$$
\begin{aligned}
	q > \sqrt{N} \implies q \ge \sqrt{N} +1 \\ 
	p > \sqrt{N} \implies p \ge \sqrt{N} +1 
\end{aligned}	
$$
Then:
$$
\begin{aligned}
		
	q \cdot p=N \implies& (\sqrt{N}+1) \cdot (\sqrt{N}+1) = N \\ 
	\implies& N + \sqrt{N} + \sqrt{N} + 1 = N \\
	\implies& 1 + N + 2\sqrt{N} = N \\
	
\end{aligned}
$$
In conclusion it is impossible for a number to have more than 1 prime number greater than $\sqrt{N}$. This leads us into another conclusion. Now let's say that q is still  a prime number that greater of equal  to $\sqrt{N}$, it implies that $p \le \sqrt{N}$

Therefore, we must only check from $[2, \sqrt{n}]$, and we can calculate the reaming factor after the search. This can reduce the conventional $O(n)$ complexity to a more efficient $O(\sqrt{n})$ and it can be used in the general instances for prime factorization, trial division and in the sieve of Eratosthenes.


### Perfect Squares, Cubes and $k$-th Roots

It is well know that we can approximate the of a number of perfect squares that are contained in  $[1,N]$ by just simply calculating  $\lfloor {\sqrt{N}} \rfloor$.  Translating this into code we would have:

```cpp
ll count = sqrt(N);
```

Which is rather simple, but we can generalize this even further. Mathematically, we can  express  the set of all number that are $k$ root that are contained in $[1,N]$ :
$$
	S = \{1^k, 2^k, 3^k, \dots, {\lfloor {\root{k}\of{N}} \rfloor}^k\}
$$

Using this fact, we can approximate the amount of $k$-th root numbers for any $k \in  \mathbb{N}$, if we know ${\root{k}\of{N}}$, or we can iterate up to the last element of $S$:

```cpp
ll count = 0;
for(ll i = 1; (ll) pow(i,k) <= N; i++) count++;
```
This algorithm runs in $O(\log{}n \root{k}\of{n})$, for larger number is is important to consider binary exponentiation instead of the builtin `pow()`.