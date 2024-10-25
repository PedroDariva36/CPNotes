#DP #Grid_Paths #Recursive #Bottom_Up

The classic grid path problems are structure like this, You have a matrix of size $N \times M$ such that $N,M \le 10^3$ , find the number of different paths that start from $(1, 1)$  and ends in $(N,M)$, since this number can exceed the size of a `64 Bit Integer`, the answer should be printed in Modulo $10^9+7$ .  Each square of the matrix hold a different character, the square with value `.` means a free square, while `#` means it is occupied, for a path to be counted it cannot pass through any occupied squares.

### Recursive Implementation

This simple recursive implementation can work on the most basic of cases, although, since it is recurse, there is a limitation  to the size of the input, for cases where $N \ge 10^3$ a Bottom Up approach may be necessary.

```cpp
const ll MOD = 1e9+7;
vector<vector<char>> g(1000, vector<char>(1000));
vector<vector<ll>> dp(1000, vector<ll>(1000, -1));
int n, m;

ll solve(int x, int y){
    if(x == n-1 && y == m-1) return 1;
    if(dp[x][y] != -1) return dp[x][y];

    ll i = 0, j = 0;

    if(x+1 < n && g[x+1][y] == '.') i = solve(x+1, y);
    if(y+1 < m && g[x][y+1] == '.') j = solve(x, y+1);

    return dp[x][y] = (i % MOD + j % MOD) % MOD;
}
```

### Bottom Up

For developing a Bottom Up approach, we must inverse the recursive rule. Instead of iterating through all paths and backtrack to the start, it is simpler to propagate the possible paths from square $(0,0)$. The answer then will be found on $(N-1,M-1)$.
This snippet is much more reliable, since the bottom up approach can be used for higher values of $N$.

```cpp 
//vector<vector<char>> g(n, vector<char>(m));
//vector<vector<ll>> dp(n, vector<ll>(m, 0));

dp[0][0] = 1;
for(int i = 0; i < n; i++){
	for(int j = 0; j < m; j++){
		for(int k: {i,i+1}){
			int l = j;
			if(k == i) l+=1;
			if(k >= n || l >= m || g[k][l] == '#') continue;
			dp[k][l] = (dp[k][l] % MOD + dp[i][j] % MOD) % MOD;
		}
	}
}
cout << dp[n-1][m-1] << endl;
```

The above spinet of code was based on [Errichto's](https://codeforces.com/profile/Errichto) code in this youtube [video](https://www.youtube.com/watch?v=FAQxdm0bTaw&t=3960s). For a more conventional but less readable snippet:

```cpp
//vector<vector<char>> g(n, vector<char>(m));
//vector<vector<ll>> dp(n, vector<ll>(m, 0));

dp[0][0] = 1;
for(int i = 0; i < n; i++){
    for(int j = 0; j < m; j++){

        if(i < n && j+1 < m && g[i][j+1] == '.')
            dp[i][j+1] = (dp[i][j+1] % MOD + dp[i][j] % MOD) % MOD;

        if(i+1 < n && j < m && g[i+1][j] == '.')
            dp[i+1][j] = (dp[i+1][j] % MOD + dp[i][j] % MOD) % MOD;
    }
    }

cout << dp[n-1][m-1] << endl;
```