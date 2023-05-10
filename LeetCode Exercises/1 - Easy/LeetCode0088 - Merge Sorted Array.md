# The problem
Here's the [link](https://leetcode.com/problems/merge-sorted-array/) to this problem.

Basically you're given two vectors, both are ordered in ascending order but there's one detail. Let's say the vectors are v1 and v2. At v1's end, there are v2.size() zeros. For example, $v_1 {1, 2, 3, 0, 0, 0}$ and $v_2 {2, 4, 5}$ are valid inputs. The goal is to merge both vectors into v1 making it sorted and with values from v2 instead of zeros.

# My first approach

I failed this one a lot of time trying to use iterators and had to seek for other people's solutions to write mine.
If you're given the size of both vectors as inputs, there might be a good reason for it. And well, if the zeros of v1 do not matter for the final result, we should make some good use of them.
It turns out that if we set up the vector from the end to the start it's pretty simple to get through this problem. Let's set three variables, one to keep track of v1's last **valid** element, one to keep track of v2's last valid element and one to keep track of v1's **actual** last element. Then we're always gonna be checking the last element of each vector and comparing them. If the highest one is from v2, then add it to the actual last element of v1 and decrease both of these indexes. Otherwise, add the highest element from v1 to its actual last position we're keeping track of and then decrease both of the indexes. We might do this while both v1 and v2 "iterators" are higher than 0.
There's two situations where we get out of this loop.
Let's start by the one where we've put all element from v2 into v1. Then there's no need to do anything, right? Because at this point, the variable that keeps track of the last actual position and the one that keeps track of the last valid element position are going to be holding the same value, so everything is already where it should be.
Now the one where we've run out of elements from v1. There's elements from v2 that are not even inside v1 yet, and we know they're going to the first indexes that remain in v1, so we just loop through the remaining elements in v2 putting them in the same position at v1.

```cpp
class Solution {

public:
	void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
		if(n == 0) return;
		int i = m - 1, j = n - 1, k = m + n - 1;
		while(i>=0 && j>=0){
			if(nums1[i] > nums2[j]){
			nums1[k--] = nums1[i--];
			}else{
				nums1[k--] = nums2[j--];
			}
		}
		while(j>=0){
			nums1[k--] = nums2[j--];
		}
	}
};
```

# Second approach

After submiting this I could just go on to the next problem but I'm my head I was like "why did I even worry about how I would sort it?". After all, there's a very effective sorting function in C++ STL and I could just merge both vectors unsorted and then sort them, after all I know exactly where the zeros start (v1's valid size) and exactly how many zeros there are (v2's size). So I tricked the problem:

```cpp
class Solution {
public:
	void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
		for(int i = m, aux = 0; aux < n; i++, aux++){
			nums1[i] = nums2[aux];
		}
		sort(nums1.begin(), nums1.end());
	}
};
```

It not only was a shorter answer. It worked MUCH better and was my first "beats 100%". Happy ending after all that headache I guess.

# What I learned from this

I think the thing I learned with this is thinking very well when problem possibly involves sorting and to explore different solutions more patiently.