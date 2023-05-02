# Definition

The time complexity is a way to measure how much time an algorithm will consume depending on its input. We denote the complexity of an algorithm using the Big O notation.

## Calculation rules

We often calculate the complexity of an algorithm in terms of $n$, $n$ being the size of the input (usually something that can be iterated through).

### Loops

Loops are indeed powerful and beginners tend to abuse their power to make their first algorithms. However, they're the main reason algorithms become slower.

The following algorithm has $O(n)$ complexity.

```cpp
for(int i = 1; i <= n; i++){
	// code
}
```

And for each k loops nested, the complexity rises up to $O(n^k)$. The following code has $O(n²)$ complexity:

```cpp
for(int i = 1; i <= n; i++){
	for(int j = 1; j <= n; j++){
		// code
	}
}
```

>[!info]
>Sometimes the complexity depends on different inputs. Take the following loop as an example:
>
>```cpp
>for(int i = 1; i <= n; i++){
>	for(int j = 1; j <= m; j++){
>		// code
>	}
>}
>```
>
>In the case above, the complexity is defined as $O(nm)$.

### Order of magnitude

Time complexity doesn't necessarily shows how many times a loop is executed, but shows only the order of magnitude. All the following algorithms have $O(n)$ complexity.

```cpp
for(int i = 1; i <= 3*n; i++){
	// code
}
```

```cpp
for(int i = 1; i <= n+5; i++){
	// code
}
```

```cpp
for(int i = 1; i <= n; i+=2){
	// code
}
```

And these have $O(n²)$:

```cpp
for(int i = 1; i <= 3*n; i++){
	for(int j = i + 1; j <= n; j++){
		// code
	}
}
```

```cpp
for(int i = 1; i <= 3*n; i++){
	for(int j = n; j >= i; j--){
		// code
	}
}
```

### Phases

Now here's something interesting: what if the algorithm has multiple loops but they're not nested? Well, then the algorithm has the complexity of the loop with the highest time complexity of them.

The following algorithm has complexity of $O(n²)$:

```cpp
for(int i = 0; i < n; i++){
	// code
}

for(int i = 1; i <= 3*n; i++){
	for(int j = i + 1; j <= n; j++){
		// code
	}
}

for(int i = 0; i < n/2; i++){
	// code
}
```

### Recursion

Time complexity of recursive functions depends on how many times the function is called and the time complexity of a single call.
Let's start with this very simple example:

```cpp
void f(int n){
	if (n==1) return;
	f(n-1);
}
```

This has a time complexity of $O(n)$ because there are n calls.
Now let's go to a more complex scenario:

```cpp
void g(int n){
	if(n==1) return;
	g(n-1);
	g(n-1);
}
```

Each call generates two others until `n==1` is reached. Therefore, the time complexity can be calculated as:

$$1 + 2+ 4 + ... + 2^{n-1} = 2^n - 1$$

In terms of complexity, it's a $O(2^n)$.

## Complexity classes

The most known complexity classes are:

- $O(1)$: the algorithm doesn't depend on the input size and runs on constant time.
- $O(\log{n})$: the algorithm usually halves the input size at each step, like in a binary search.
- $O(\sqrt{n})$: faster than $O(n)$ but slower than $O(\log{n})$.
- $O(n)$: the classic linear algorithm. Accesses each input index at least once.
- $O(n\log{n})$: there's two main reasons some algorithms run in this time-complexity, the first one is that the input is sorted at some point, because the best sorting algorithms usually are $O(n\log{n})$, and the other possibility is that a data structure where operations take $O(\log{n})$ time, like most trees, is being used.
- $O(n²)$: mostly indicates two nested loops.
- $O(n³)$: mostly indicates triple nested loops.
- $O(2^n)$: mostly indicates an iteration through all subsets of the input.
- $O(n!)$: mostly indicates an iteration through all permutations of the input.

>[!info]
>Notice how the complexity classes are ordered crescently in terms of time.

For further comprehension about time complexity check the [[Maximum subarray sum]] problem explanation.

---

