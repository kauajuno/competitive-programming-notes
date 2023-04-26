# The exercise
[Here's the link to this exercise](https://leetcode.com/problems/two-sum/)

Given an array of integers `nums` and an integer `target`, return _indices of the two numbers such that they add up to `target`_.

# Optimal approach

There's an $O(n)$ solution for this problem, where each number doesn't need to be analyzed more than once, at the cost of some memory.
In this approach, a map is used to store values from the array and their indexes. Starting from the begin of the array, we try to find the number that would perfectly match that one to reach the target in the map we created. If it is not found, then the number we just analyzed is put on the map as a key, and the value is its index. We do that because if it happens that this number is the perfect match to any other in the array, it's gonna be found in the map with just a little search. And the cycle goes on.

>[!info]
>Maps/dictionaries queries are done in $O(1)$

```cpp
vector<int> sum_two(vector<int>& vec, int target){
	unordered_map<int, int> map;
	int complement;
	for(int i = 0; i < vec.size(); i++){
		complement = target - vec[i];
		if(map.find(complement) != map.end())
			return {map[complement], i};
		map[vec[i]] = i;
	}
	return {-1, -1};
}
```

# What I've learned here

Maps are very interesting structures, excellent to search key->value types. Given a `map.find(complement)`, it will search for the value with key `complement` in the map. If it doesn't find anything, it returns an iterator to the end of the map, same as `map.end()`.

---

#datastructures #leetcode #solved #easy