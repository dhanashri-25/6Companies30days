# Minimum Moves to Equal Array Elements II
[Problem Link](https://leetcode.com/problems/minimum-moves-to-equal-array-elements-ii/description/)

Given an integer array `nums` of size `n`, return the minimum number of moves required to make all array elements equal. In one move, you can increment or decrement an element of the array by 1.

**Input:**
```
nums = [1, 2, 3]
```

**Output:**
```
2
```

**Explanation:**
Only two moves are needed (remember each move increments or decrements one element):
- [1, 2, 3] → [2, 2, 3] → [2, 2, 2]

**Example 2:**

**Input:**
```
nums = [1, 10, 2, 9]
```

**Output:**
```
16
```

### Solution Explanation

The best way to minimize the moves required to make all the elements equal is to gather everyone around the **median** value of the array. 

#### Why Median?
- The median minimizes the sum of absolute differences between all elements and the selected point. This is because the sum of absolute differences is smallest when you select the median.
- This is a well-known property from statistics, and it works perfectly for this problem.

### Approach

1. **Sort the Array**: Sorting helps to easily find the median element.
2. **Find the Median**: 
   - If the array size `n` is odd, the median is the middle element of the sorted array.
   - If `n` is even, the median can be any of the two middle elements, but the result will be the same as either choice.
3. **Calculate Moves**: Iterate through the array and calculate the total number of moves (sum of absolute differences) to make each element equal to the median.

### Code

```java
class Solution {
    public int minMoves2(int[] nums) {
        int n = nums.length;
        Arrays.sort(nums);  // Sort the array to find the median
        int median = nums[n / 2];  // Median is the middle element in the sorted array
        int ans = 0;
        
        // Calculate the sum of absolute differences from the median
        for (int i = 0; i < n; i++) {
            ans += Math.abs(nums[i] - median);
        }
        
        return ans;  // Return the total number of moves
    }
}
```

### Time Complexity
- Sorting the array takes `O(n log n)`.
- Calculating the total moves takes `O(n)`.

Thus, the overall time complexity is `O(n log n)`.

---

### Explanation in Simple Terms:

Imagine you have a group of friends standing in a straight line. You want them all to meet at one point with the least amount of walking. If everyone gathers at the **median** of their positions, the total walking distance for the group will always be the smallest possible. 

This is why finding the median and summing the absolute distances from each friend to the median gives us the minimum number of moves.

### Accepted Solution
![Screenshot 2025-01-04 153042](https://github.com/user-attachments/assets/d7d4bba9-68b6-483b-a1d1-79cac2826b16)
