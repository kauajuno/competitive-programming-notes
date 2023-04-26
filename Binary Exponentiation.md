The main idea behind the binary exponentiation is to split the work that would have to be done by multiplicating a number by itself for either a large base or exponent via the binary representation of the exponent.
$$2^{15} = 2^{1111\tiny2} = 2^8 . 2^4 . 2^2. 2^1$$
But it doesn't look that easy yet, because now we need to calculate 4 more powers. But there's an easy way to calculate each one of them:
$$\begin{align}
2^1 &= 2 \\
2^2 &= \left(2^1\right)^2 = 2^2 = 4 \\
2^4 &= \left(2^2\right)^2 = 4^2 = 16 \\
2^8 &= \left(2^4\right)^2 = 16^2 = 256
\end{align}$$
Each element in the sequence is the square of the previous one. Then all you need to do is calculate this multiplication and everything is set.
$$2^{15} = 2^{8} . 2^{4} . 2^{2} . 2^{1} = 256 . 16 . 4 . 2 = 32768$$
### Recursive approach
```cpp
long long binpow(long long a, long long b) {
    if (b == 0)
        return 1;
    long long res = binpow(a, b / 2);
    if (b % 2)
        return res * res * a;
    else
        return res * res;
}
```

### Non-recursive approach
```cpp
long long binpow(long long a, long long b) {
    long long res = 1;
    while (b > 0) {
        if (b & 1)
            res = res * a;
        a = a * a;
        b >>= 1;
    }
    return res;
}
```

