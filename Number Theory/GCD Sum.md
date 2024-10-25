#GCD #number_Theory 

### GCD Summation

Let $S(n)$ be the summation of all the greatest common divisors of $i$ and $n$ were $i \in  \{ i \dots \}$:

$$ 
	S(n) = gcd(1,n) +  gcd(2,n) + gcd(3,n) \dots gcd(n,n)
$$

We can observe 2 facts about the above sequence:
	1. All the elements of the series are divisors of $n$;
	2. The





### Solving GCDEX

Let's say $n = 6$, the loop will sum this values
$$
\begin{aligned}
1 \implies & gcd(1,2) + gcd(1,3) + gcd(1,4) + gcd(1,5) + gcd(1,6) \\
2 \implies & gcd(2,3) + gcd(2,4) + gcd(2,5) + gcd(2,6) \\
3 \implies & gcd(3,4) + gcd(3,5) + gcd(3,6) \\
4 \implies & gcd(4,5) + gcd(4,6) \\
5 \implies & gcd(5,6) \\
\end{aligned}
$$
We can then rearrange this into:
$$
\begin{aligned}
1 \implies & gcd(1,2) \\
2 \implies & gcd(1,3) + gcd(2,3) \\
3 \implies & gcd(1,4) + gcd(2,4) + gcd(3,4) \\
4 \implies & gcd(1,5) + gcd(2,5) + gcd(3,5) + gcd(4,5) \\
5 \implies & gcd(1,6) + gcd(2,6) + gcd(3,6) + gcd(4,6) + gcd(5,6) \\
\end{aligned}
$$

We can now see the emerging pattern, Let's then use the **gcd sum function**, and simplify this expression :

$$
\begin{aligned}
1 \implies & \sum_{d\mid2}d*\phi(\frac{2}{d}) \; -1  \\
2 \implies & \sum_{d\mid3}d*\phi(\frac{3}{d}) \; -1  \\
3 \implies & \sum_{d\mid4}d*\phi(\frac{4}{d}) \; -1  \\
4 \implies & \sum_{d\mid5}d*\phi(\frac{5}{d}) \; -1  \\
5 \implies & \sum_{d\mid6}d*\phi(\frac{6}{d}) \; -1  \\
\end{aligned}
$$

now we can just generalize it for any $n$, giving us the formula:
$$
	\sum_{k=1}^{n} \sum_{d\mid{k}}d*\phi(\frac{k}{d}) \; - n
$$

#TODO
RESEARCH:
- https://heneos.medium.com/project-euler-625-8fc80e6ffe58
- https://planetmath.org/dirichlethyperbolamethod
- https://personalpages.manchester.ac.uk/staff/mark.coleman/old/MATH41022/Present/notes/notes%204%202017-18%20hyper%20Mthd%20w%20figs.pdf
- https://math.stackexchange.com/questions/316376/how-to-calculate-these-totient-summation-sums-efficiently
- https://math.stackexchange.com/questions/4782264/complexity-of-recursion-with-floor-division-fn-fn-sum-m-2n-f-left/4786359#4786359
- https://github.com/trizen/project-euler/blob/master/Perl/625%20gcd%20sum.pl
- https://oeis.org/A064018

