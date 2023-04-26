# The exercise
[Here's the link to the exercise](https://leetcode.com/problems/palindrome-number/)

Given an integer `x`, return `true` _if_ `x` _is a_ **palindrome**, and `false` _otherwise_.

# First approach

In my first approach, I tried to think of how to separate the numbers in a simple way. My idea was to split the digits in a list and, after each digit was in the list, I'd go comparing the first and the last element in the list until there were only 1 or no digits in the list. If at some point the first and the last digit were different, I'd return false, the number **is not** a palindrome. Otherwise, the program would procceed naturally until the end, where it returns true.

It ended up being a pretty slow approach.

# Optimal appoach

First things first, we can make two assumptions about palindromes besides its main definition:
- Negative numbers are never palindromes.
- Numbers ended in 0 can never be palindromes (except for 0 itself).
Given these two things, let's make a condition that can discard these types of numbers at very first: `if(x < 0 || x != 0 && x%10 == 0) return false`. First it checks if a number is a multiple of 10 (ends in zero). If it is, then `false` is being returned no matter what. If it's not, it'll check if the number is negative. If it is, then `false` is being returned no matter what. If it's not, then the condition itself is false and the code moves along.

Now there's a very interesting way to check if the number is a palindrome or not, that involves no data structures at all.

Let's take, for example. The number 1221.
If our intention is just to split that number and get only the first half, we could divide it by 100 and voilá. But what if we wanted the two halves?
Let's create a variable to store the other half. `int half = 0;`. Now, we're getting that half into this variable, digit by digit. To store the first one we could just get in with `half = number / 10;`, but what's next for the other digits? You might think that, if we had a counter or something, that increase in a `counter *= 10` logic and that keeps multiplying the number that is going to come into this variable it could work. But in that case, we would end up with a reversed half: 12 and 21, in our case.
The solution here is to make sure that, for each new digit that comes into the variable, the ones that are already here have to move left by one place. And we can achieve this result with the following code:

```cpp
class Solution {
public:
	bool isPalindrome(int x) {
		if(x < 0 || x != 0 && x % 10 == 0)
			return false;
		int half = 0;
		while(x > half){
			half = half * 10 + x % 10;
			x /= 10;
		}
		return x == half;
	}
};
```

But then there's something else, what if `x` has an odd number of digits?
Well, then we gotta ignore the one in the middle. It doesn't change anything, right? 11011, 11111, 11211, 11311, 11411, and so on, they're all palindromes, and the only thing changing is the digit in the middle because it doesn't matter.
Well then, the middle digit will always go to the half variable, because the loop only stops when `x` is less than `half`, so the `half` one gotta have one more digit than `x`. Then all we need to do is compare `x` to `half` minus one digit:

```cpp
class Solution {
public:
	bool isPalindrome(int x) {
		if(x < 0 || x != 0 && x % 10 == 0)
			return false;
		int half = 0;
		while(x > half){
			half = half * 10 + x % 10;
			x /= 10;
		}
		return x == half || x == half / 10;
	}
};
```

# What I've learned here

Actually the main thing I learned from this exercise was the operator precedency thing. I always relied just on parenthesis but now knowing that `&&` has a higher precedency priority than `||` will make me go faster through conditionals.  

---

#datastructures #leetcode #solved #easy