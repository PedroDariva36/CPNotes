#DP #Bottom_Up #Coin_Toss_Probability


Given a set with $N$ coins, and an array $a$, where $a_i$ represents the probability of a coin to be heads when it's tossed, calculate the probability of event to happen:

### Toss all coins, probability of more than half to be heads

In order for us to calculate that probability we need to memoize all the possibilities or reaching states of more heads than tails while throwing the coins:

```cpp
vector<double> a(n);
vector<double> dp(n+1);
```

This algorithm works by calculating what is the probability of at least $k$ heads to be tossed, with any number of coins, that will be stored in the $DP$ vector. 

In order for us to calculate whether we can get to a state where $i$ coins are heads we need to know two probabilities:
* **The Tails State**: the probability of we tossing a coin it been tails and we maintain the state we are currently at, 
* **The Head State**: the probability of reaching $i-1$ tossed head, so that tossing another coin can make us reach the $i$-th state
So our answer will be the sum of those probabilities.

When it comes to implementation, we will use de same format as a Knapsack problem.
In order to not repeat values, we iterate from $N+1$ heads, to $1$ head. And the base case of the recursion should be 1, since we always start from a state where we don't toss any coins, the probability of achieving state 0 is 100%; 

```cpp
dp[0] = 1;
for(auto c: a){
	for(int i = n+1; i > 0; i--){
		dp[i] = dp[i]*(1-c) + dp[i-1]*c;
	}
}
```

In order to find the the probability of tossing more heads than tails, we now only need to look to the first position that is after the middle point of the array, we can do that by looking in `dp[n/2+1]`;
