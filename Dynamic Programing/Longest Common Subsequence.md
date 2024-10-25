#DP #LCM #Printing_DP #Recursive #Bottom_Up

### Base algorithm:

The basic implementation begins with 2 strings and the declaration of a simple matrix, that will be used for memoizing the solution:

```cpp
string s,t;
cin >> s >> t; 
vector<vector<int>> dp(s.length()+1, vector<int>(t.length()+1,0));
```

The algorithm can be expressed with this simple recursive rule:
$$
LCS(i,j) = 
\begin{cases}
	0, & \text{if }  i = 0 \lor j = 0\\
    LCS(i-1,j-1) + 1, & \text{if } s[i] = t[j]\\
    MAX(LCS(i-1,j),LCS(i,j-1)), & \text{otherwise}
\end{cases}
$$

Following the rule, we can then invert it in order implement the same basic idea in a Bottom Up approach:

```cpp
for(int i = 0; i < s.length(); i++){
	for(int j = 0; j < t.length(); j++){
		if(s[i] == t[j])
			dp[i+1][j+1] = max(dp[i+1][j+1], dp[i][j] + 1);	

		dp[i+1][j] = max(dp[i+1][j], dp[i][j]);
		dp[i][j+1] = max(dp[i][j+1], dp[i][j]);

	}
}
```

Now in order to find the  answer we can search the matrix and get the **size** of the longest common subsequence:

```cpp
int asw = 0;
for(int i = 0; i <= s.length(); i++){
    for(int j = 0; j <= t.length(); j++){
        asw  = max(asw, dp[i][j]){  
    }
}
```

This algorithms runs in $O(n^2)$ both in Speed and Memory, although using a bottom Up approach, allows it to be used for larger strings.

### Printing the actual subsequence:

In order to print the subsequence the most common approach is to create a auxiliary matrix $f$ with the same dimensions as $DP$.

```cpp
typedef pii = pair<int,int>;

string s,t;
cin >> s >> t; 
vector<vector<int>> dp(s.length()+1, vector<int>(t.length()+1, 0));
vector<vector<pii>> f(s.length()+1, vector<pii>(t.length()+1, {0,0}));
```

Then we accommodate the algorithm a bit. Now every time a better answer is found, the pair $(i,j)$  is stored in $f$, similarly to what is used to store the structure of a tree in graph problems :  

```cpp
for(int i = 0; i < s.length(); i++){
	for(int j = 0; j < t.length(); j++){
		if(s[i] == t[j])
			if(dp[i+1][j+1] < dp[i][j] + 1){
				dp[i+1][j+1] = dp[i][j] + 1;
				f[i+1][j+1] = {i,j}; 
			}                

		if(dp[i+1][j] < dp[i][j]){
			dp[i+1][j] = dp[i][j];
			f[i+1][j] = {i,j};
		}

		if(dp[i][j+1] < dp[i][j]){
			dp[i][j+1] = dp[i][j];
			f[i][j+1] = {i,j};
		}
	}
}
```

Then find the answer and by searching the matrix, in case the position remains the same we know that there are no two matching characters in both $s$ and $t$ :

```cpp
int asw = 0;
pii pos = {0,0};
for(int i = 0; i <= s.length(); i++){
    for(int j = 0; j <= t.length(); j++){
        if(asw < dp[i][j]){  
            asw = dp[i][j];
            pos = {i,j};
        }
    }
}

if(pos.first == 0 && pos.second == 0){
    cout << endl;
    continue;
}
```

Finally we can backtrack and for every diagonal increase we find in $DP$ we add a character. Using this method, the answer will  be in reverse, so we simply reorder it.

``` cpp
vector<char> a; 
auto cur = pos; 
while (cur.first != 0 && cur.second != 0) {
    int i = cur.first;
    int j = cur.second;
    pii prev = f[i][j];
    
    if(prev == make_pair(i-1,j-1)) 
	    a.pb(s[i-1]);
    
    cur = prev;
}
reverse(all(a));    


for(auto &i: a) 
	cout << i;
cout << endl;

}
```

This algorithms runs in $O(n^2)$ both in Speed and Memory.
