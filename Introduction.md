Competitive programming combines design and implementation of algorithms.
Design of algorithms consists of problem solving and mathematical thinking, while the implementation requires good programming skills. It is good to be straightforward and concise as a competitor in the competitive programming world.

## Programming languages

The most used programming languages for competitive programming are C++, Python and Java.
Most people think C++ is the best language for competitive programming contests because of its powerful standard library and efficiency. But in the other hand, a language such as Python might come in handy for large integers processing because of its built-in operations.

## C++ code template

```cpp
#include <bits/stdc++.h>

using namespace std;

int main(){
	// solution
}
```

Let's see what those two first lines do:

```cpp
#include <bits/stdc++.h>
```

This is useful because it includes all the C++ STL (Standard Template Libraries) in the code, so that the coder doesn't need to be worried about including a lot of libraries for each different thing they're gonna use in the code. It's not a good practice for other purposes but it is a great time saver.

```cpp
using namespace std;
```

Another time saver: this is useful because it allows the programmer to code inputs and outputs typing less characters. ```std::cout``` can be written as just  ```cout```.

## Input and output

There are some lines that can be implemented to make I/O operations faster in C++.

```cpp
ios::sync_with_stdio(0);
cin.tie(0);
```

>[!info]
>printf and scanf from C still can be used and they're usually faster, but harder to manipulate.

Sometimes it is useful to read an entire line (that might even have some spaces in between) from the input at once. The getline function comes handy at these situations:

```cpp
string s;
getline(cin, s);
```

For unknown amounts of data, a loop such as this one can help:

```cpp
while(cin >> x){
	// loop
}
```

## Numbers

### Integers

The most used integer type is int, which, as a 32-bit type, can hold values from -2³¹ to 2³¹ - 1. However, this is frequently not enough, there's lots of problems where there's really big numbers to deal with. So there's long long.

```cpp
long long x = 12345678987654321LL;
```

A common mistake made by beginners is trying to store operations between ints in a long long without a cast.

```cpp
int a = 123456789;
long long b = a * a;
cout << b << "\n"; // -1757895751
```

This happens because operations between int-typed values generate int-typed values. Then the best solution for this is either changing ```a``` to ```long long``` or casting one of the values of the operations as a ```long long```.

>[!info]
>This is pretty much unusual but if long long is still not enough, there's a 128-bit integer type which can store much larger values, it's the ```__int128_t```.

### Floating point numbers

There are two main floating point types in cp: ```double```, the 64-bit one; and ```long double```, the 80-bit one which is more accurate.
Anyway, floating point numbers can sometimes be confusing. Let's take the following code as an example:

```cpp
double x = 0.3 * 3 + 0.1;
printf("%.20f\n", x); // 0.99999999999999988898
```

This happens due to rounding errors. The value is very, very close to 1, but it actually isn't. This implies that comparison operations between floating point numbers might be **very** risky if done in the naive approach.
A good way to get through this is checking if the difference between the two numbers in question is less than some $\varepsilon$ constant that represents a very small number (let's suppose $\varepsilon = 10^{-9}$).

```cpp
if(abs(a-b) < 1e-9){
	// a and b are equal
}
```

## Modular arithmetic

Sometimes, given a m value, problems are gonna ask you to output some number modulo m. What does that mean?
$x \bmod m$ is the remainder when x is divided by m. For example:
$$13\bmod2 = 1$$
$$18 \bmod 3 = 0$$
The idea is that even if the actual answer is very large, it suffices to use the types int and long long.
There are some interesting properties in modular arithmetic:
$$(a+b)\bmod m = (a \bmod m + b \bmod m) \bmod m$$
$$(a-b)\bmod m = (a \bmod m - b \bmod m) \bmod m$$
$$(a\cdot b)\bmod m = (a \bmod m \cdot b \bmod m) \bmod m$$
The application of those is getting the remainder without making the operation, this helps preventing overflows.

The following code calculates $n! \bmod m$ using the third property listed above:

```cpp
long long x = 1;
for(int i = 2; i <= n; i++){
	x = (x*i) % m;
}
```

There's yet another problem: what if we want $x \bmod m$ given a negative $x$? Usually we should get a number between $0$ and $m - 1$ as a remainder.
Well, a simple conditional can solve that:

```cpp
x = x % m;
if(x < 0) x += m;
```

## Shortening code

Shortening code is often needed to write it faster. Time is one of the most precious aspects in competitive programming contests. There are some tricks to get your code shorter.

### Type names

The ```typedef``` command is used to rename types in C/C++. The most notable example is:

```cpp
typedef long long ll;
```

With the line above, this code:

```cpp
long long a = 9138903180918LL;
long long b = 8943728917280LL;
cout << a*b << "\n";
```

Can be shortened into this one:

```cpp
ll a = 9138903180918LL;
ll b = 8943728917280LL;
cout << a*b << "\n";
```

And this extends to even more complex types, such as:

```cpp
typedef vector<int> vi;
typedef pair<int, int> pi;
```

### Macros

Another way to write shorter code is to define macros. A macro means that some strings in the code are going to be changed before the compilation. The ```#define``` keyword is used to create macros in C/C++.

With these lines:

```cpp
#define F first
#define S second
#define PB push_back
#define MP make_pair
```

This code:

```cpp
v.push_back(make_pair(y1,x1));
v.push_back(make_pair(y2,x2));
int d = v[i].first+v[i].second;
```

Can be shortened into this one:

```cpp
v.PB(MP(y1,x1));
v.PB(MP(y2,x2));
int d = v[i].F+v[i].S;
```

>[!info]
>Macros can be rather confusing at times, so it's always important to define names that are somehow related to the original content.

Macros can have parameters, making it possible to shorten more complex structures. With this line:

```cpp
#define REP(i,a,b) for (int i = a; i <= b; i++)
```

The two following codes are equivalent:

```cpp
for(int i = a; i <= b; i++){
	search(i);
}
```

```cpp
REP(i,1,n){
	search(i);
}
```

Even though macros are very powerfull, it requires some carefulness to deal with it, cause sometimes it causes problems that are really hard to debug.
Let's take the following code as an example:

```cpp
#define SQ(a) a*a
```

It would generate a wrong answer to the following call:

```cpp
cout << SQ(3+3) << \n;
// 3+3*3+3 = 15
// expected: 36
```

A right way to express the macro would be:

```cpp
#define SQ(a) (a)*(a)
```

```cpp
cout << SQ(3+3) << \n;
// (3+3)*(3+3) = 6*6 = 36
```

## Mathematics

Mathematics plays an important role in competitive programming. Here are some important matematical concepts.

### Sum formulas

Each sum of the form

$$\sum_{n=1}^{n} {x^k} = 1^k + 2^k + 3^k + ... + n^k$$

where k is a positive integer, has a closed-form formula that is a polynomial of degree $k+1$, such as:

$$\sum_{x=1}^{n} x = 1 + 2 + 3 + ... + n = \frac{n(n+1)}{2}$$
$$\sum_{x=1}^{n} x² = 1² + 2² + 3² + ... + n² = \frac{n(n+1)(2n+1)}{6}$$

### Arithmetic progression

An arithmetic progression is a sequence of numbers where the difference between any two consecutive numbers is constant. $3, 7, 11, 15$ is an arithmetic progression.
The sum of an arithmetic progression can be calculated as:

$$S = a + ... + b = \frac{n(a+b)}{2}$$
where $a$ is the first number, $b$ is the last one and $n$ is the number of elements in the sequence.
There's also a formula for situations where you don't have the last element, it is:
$$S = \frac{n(2a + (n-1)d)}{2}$$
where d is the difference between each consecutive element.

### Geometric progression

A geometric progression is a sequence of numbers where the ratio between any two consecutive numbers is constant. For example: $3, 6, 12, 24$. The sum of a GP can be calculated using this formula:

$$a + ak + ak² + ... + b = \frac{bk - a}{k-1}$$

This formula can be derived. Let

$$S = a + ak + ak² + ... + b$$

Multiplying both sides by k, we get

$$kS = ak + ak² + ak³ + ... + bk$$

Then removing S from both sides, we get

$$kS - S = bk - a$$

### Harmonic sum

WIP

### Set theory

A set is a collection of elements. For example, the set
$$X = [2, 4, 7]$$
contains elements 2, 4 and 7. The symbol $\emptyset$ denotes an empty set, and $|S|$ denotes the size of a set $S$. $|X| = 3$ for the example above. To denote if a element is in a set or not, we use $\in$ and $\notin$. For the example above, $4 \in X$ and $5 \notin X$.
New sets can be constructed using set operations:
- Intersection: $A \cap B$.
- Union: $A \cup B$.
- Complement: $\bar{A}$. Depends on the **universal set** as well. If the universal set is $[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]$ and $A = [1, 2, 3]$, then $\bar{A} = [4, 5, 6, 7, 8, 9, 10]$. 
- Difference: $A \backslash B$ or $A \cap \bar{B}$. Consists of elements that are in A but not in B.

If each element of a set A is contained in S, it is possible to affirm that $A \subset S$. Same thing goes the other way with $S \supset A$.

A set $S$ always has $2^{|S|}$ possible subsets. For example, the subsets of $S = [1, 2, 3]$ are:
- $\emptyset$
- $[1]$
- $[2]$
- $[3]$
- $[1, 2]$
- $[1, 3]$
- $[2, 3]$
- $S$

It's also possible to create a set using the rule of form $\{f(n) :  n \in S\}$. For example, the set $\{2n : n \in \mathbb{N} \}$ contains every even integer.

### Logic

Logic expressions can be either true or false. This looks pretty simples but logical expressions can get really complex sometimes. Not something that happens that often in competitive programming, knowing the basics is already a nice kickoff:

There are four main logical operations:

- AND: in this binary operator, the result is true only if both arguments are true, otherwise it's false.
- OR: in this one, the result is false only if both arguments are false, otherwise is true.
- NOT: this is an unary operator, if the argument passed is true it turns out to be false, the same goes the other way.
- IMPLIES: if a true argument implies in false, then the expression is false, otherwise it is true.

| $A$ | $B$ | $\lnot{A}$ | $\lnot{B}$ | $A \land B$ | $A \lor B$ | $A \implies B$ | $A \iff B$ |
|---|---|---|---|---|---|---|---|
| $0$ | $0$ | $1$ | $1$ | $0$ | $1$ | $1$ | $1$ |
| $0$ | $1$ | $1$ | $0$ | $0$ | $1$ | $1$ | $0$ |
| $1$ | $0$ | $0$ | $1$ | $0$ | $1$ | $0$ | $0$ |
| $1$ | $1$ | $0$ | $0$ | $1$ | $0$ | $1$ | $1$ |

These logical expressions can be denominated as predicates if they have parameters. Their results can be true or false depending on the parameters they receive. Let's suppose we have a $O(x)$ predicate that determines if a number is odd. It would return `true` for $3$ and `false` for $10$, for example.

There's also quantifiers in logic that connects logical expressions to the elements of a set. The two quantifiers are **for all** ($\forall$) and **there is** ($\thereis$).

### Functions

Functions basically transform inputs in outputs following a rule or set of rules. There are some must-know functions for competitive programming:

- $\lceil x \rceil$: rounds the number $x$ up one integer.
- $\lfloor x \rfloor$: rounds the number $x$ down one integer.
- min(collection): returns the lowest value from a collection. For example: given the set $(1, 2, 3, 4)$, the function will return $1$.
- max(collection): return the highest value from a collection. For example: given the set from the previous example, the function will return $4$.
- fib$(n)$: returns the number at the $n$th position in the fibonacci numbers sequence. For example: fib$(5)$ = $5$. It's defined recursively as:
$$f(0) = 0$$
$$f(1) = 1$$
$$f(n) = f(n-1) + f(n-2)$$

>[!info]
>There's a non-recursive formula called Binet' formula that also calculates fibonacci numbers:
>$$f(n) = \frac{(1 + \sqrt{5})^{n} - (1 - \sqrt{5})^{n}}{2^{n}\sqrt{5}}$$

### Logarithms

Logarithms are kinda abstract at first, but basically we can affirm $log_{k}{(x)} = a$ when $k^a = x$. We can divide $x$ by $k$ exactly $a$ times before reaching $1$.
$$\log_{2}{32} = 5$$
$$32 \rightarrow 16 \rightarrow 8 \rightarrow 4 \rightarrow 2 \rightarrow 1$$

>[!info]
>Note that there's exactly five arrows.

Here are some other useful logarithm properties:

$$log_k{(ab)} = log_k(a) + log_k(b)$$
$$log_k{(x^n)} = n \cdot log_k(x)$$
$$log_k{(\frac{a}{b})} = log_k(a) - log_k(b)$$
$$log_u{(x)} = \frac{log_k{(x)}}{log_k{(u)}}$$

Other two things that are important to know about logarithms:

- When the base of an logarithm is "hidden", we make an assumption that it is a $log_{10}$.
- When the logarithm is denoted as $\ln$, it refers to a natural logarithm, in which the base is $e \approx 2.71828$, the euler number.


