### Conventional
A simple code for getting the minimum and maximum prefix sum:

```cpp
ll sum = 0,l = 0, r = 0;
for(int i = 0; i < n; i++){
	pr += a[i];
	l = min(pr,l);
	r = max(pr-l, r);
}
```
+ the variable sum holds the prefix sum;
+  `l` holds the minimum and `r` holds the maximum;
+ Time complexity of : $\mathcal{O}(n)$


### Optimized

``` cpp
ll l = 0, r = 0;
for(int i = 0; i < n; i++){
	l = min(0ll, l+a[i]);
	r = max(0ll, r+a[i]);
}
```

### Uses

This algorithm can be used with certain limitations to calculate all possible subarray sums adding the values of `l` and `r` to a `Set` should result in all possible values that can be achieved by summing subarrays.

