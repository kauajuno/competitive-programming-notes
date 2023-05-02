# The problem

This is an easy to understand problem with multiple time-complexity approaches being possible to solve it. Basically we're having an array as an input and we gotta find the subarray that has the maximum sum value and return it. It can be kinda tricky considering that the array can have negative integers as well. Another important spot to look at is that a subarray with no elements is also a possible solution, so the maximum subarray sum is at least 0.

# Solutions

## The $O(n³)$ approach

The brute force solution is to go through all possible subarrays and keep comparing the sums to see which value ends up being the highest. This takes three nested loops.

```cpp
int best = 0;
for(int a = 0; a < n; a++){
	for(int b = a; b < n; b++){
		int sum = 0;
		for(int k = a; k <= b; k++){
			sum += array[k];
		}
		best = max(best, sum);
	}
}
return best;
```

## The $O(n²)$ approach

Follows almost the same logic as the previous one except that the innermost loop is removed as it is really unnecessary and the best sum value can be checked at the same time that the subarray goes increasing.

```cpp
int best = 0;
for(int a = 0; a < n; a++){
	int sum = 0;
	for(int b = a; b < n; b++){
		sum += array[b];
		best = max(best, sum);
	}
}
return best;
```

## The $O(n)$ approach

This is tricky to understand but really worth the effort.