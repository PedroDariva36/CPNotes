#DP #Prefixes

In this problem we wish to count all the subarrays whose sum is equal to their length. To do this we use prefix sums. First a little algebraic manipulation is in order.

 $$
	\begin{aligned}
		\\
		&\forall \; l,r  \; \in \{ 0, \cdots, n-1 \} \; ; \; l <= r  \\
		&s(l,r) = \sum_{l}^{r} a[l] \\
	\end{aligned}
$$
In this problem we look for all subarrays $s(l,r) = r-l+1$, in other words, all subarrays where $s(l,r) - (r-l+1) = 0$;

We can then fix  $l = 0$ and simplify the expression, so now we change the sum function into a prefix sum (denoted by $p$), and we have the expression $p[i] - (i+1) = 0$, so by testing all positions up to $n$ we count all the subarrays we a prefix of 0;

This only fixed half of the problem, now let's review the above formula in detail, if we in fact  bring back the old formula, and instead of fixing $l$ we isolate all terms dependent on it, $(p[i] - p[j] + a[j]) - (i-j+1) = 0$, thus $p[i] - (i+1) = p[j-1] - j$; 

In the code, evaluating the expression $p[j-1] - j$ cannot be done because for position 0 we have $p[-1]$, therefore we can just define it as the empty subarray, so we add $m[0] = 1$ in the code;

Let's also be attentive to the fact that the values of $j$ we can look is limited by $i$, so we said in the definition of $l$ and $r$,  therefore we can only look at values that are already computed. That is why the values of the conditions are feed to $m$, in order to efficiently memoize the values of $(p[j-1] - j)$.

Another neat trick is that we can do a variable change in $j$, so that $j = k+1$, now the other side of the equation ca be rewritten as $(p[k] - k+1) \; ; k < i;$ . So we can directly feed the value of the iteration to the map;

Now for the calculation of the answer, we count the result of every position up to n, and then all the possible pair for every value; This can be done online as shown bellow, or by calculating the binomial coefficient of every value;


$$

	asw = \sum_{ c \, \in \, m} \binom{c}{2} = \sum_{ c \, \in \, m} \frac{c*(c-1)}{2}

$$



```cpp
int n;
cin >> n;
vector<int> a(n);
vector<int> pref(n);
char aux;

for(int i = 0, sum = 0; i < n; i++){
	cin >> aux;
	a[i] = aux-'0';
	sum += a[i];
	pref[i] = sum;
}


map<ll,ll> m;
m[0] = 1;
ll asw = 0;
for(int i = 0; i < n; i++)
	asw += m[pref[i]-(i+1)]++;

cout << asw << endl;
```






Problem:
- https://codeforces.com/contest/1398