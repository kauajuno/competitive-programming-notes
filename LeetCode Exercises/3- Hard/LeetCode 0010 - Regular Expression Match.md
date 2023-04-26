# The exercise
[Here's the link to this exercise](https://leetcode.com/problems/regular-expression-matching/)

Given an input string `s` and a pattern `p`, implement regular expression matching with support for `'.'` and `'*'` where:

-   `'.'` Matches any single character.​​​​
-   `'*'` Matches zero or more of the preceding element.

The matching should cover the **entire** input string (not partial).

# Things to look at

It was hard even to understand this exercise's logic at first. But here it is: the `'.'` is like a joker card, it can substitute any other character. And the `'*'` is in fact like a multiplicator (that can also multiply by 0, keep that in mind).

Here are some examples that can help to understand this deeper:
- any strings that go in comparison with `".*"` should result in true, because it is an unlimited repetition of a character that can replace any other. Therefore, `".*"` is equivalent to any string.
- `"aaaaaaaaaaaaaaaaaaaaaaaaaaazaaaaaaaaaakwqejioc"` and `".*c"`  should result in `true`. Any string ended in `'c'` with that `p` string should be true.

---
#unsolved #hard