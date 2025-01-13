# 532. K-diff Pairs in an Array
[problem link](https://leetcode.com/problems/k-diff-pairs-in-an-array/)

## Problem Statement

Given an array of integers `nums` and an integer `k`, return the number of unique k-diff pairs in the array.

A **k-diff pair** is an integer pair `(nums[i], nums[j])`, where the following are true:
- `0 <= i, j < nums.length`
- `i != j`
- `|nums[i] - nums[j]| == k`

Notice that `|val|` denotes the absolute value of `val`.

---

### Example 1

**Input:**  
`nums = [3,1,4,1,5], k = 2`  
**Output:**  
`2`  
**Explanation:**  
There are two 2-diff pairs in the array: `(1, 3)` and `(3, 5)`.  
Although there are two `1`s in the input, we should only return the number of unique pairs.

---

### Example 2

**Input:**  
`nums = [1,2,3,4,5], k = 1`  
**Output:**  
`4`  
**Explanation:**  
There are four 1-diff pairs in the array: `(1, 2)`, `(2, 3)`, `(3, 4)`, and `(4, 5)`.

---

### Example 3

**Input:**  
`nums = [1,3,1,5,4], k = 0`  
**Output:**  
`1`  
**Explanation:**  
There is one 0-diff pair in the array: `(1, 1)`.

---

## Constraints

- `1 <= nums.length <= 10^4`
- `-10^7 <= nums[i] <= 10^7`
- `0 <= k <= 10^7`

---

## Approach and Solution

The solution follows these steps:

1. **Sort the Array:**  
   Sort `nums` to efficiently handle duplicates and use a two-pointer or nested loop approach.
   
2. **Iterate Through the Array:**  
   Use an outer loop to fix one number and an inner loop to find pairs with the required difference `k`.

3. **Skip Duplicates:**  
   Ensure each pair is unique by skipping duplicates in the outer loop.

4. **Break Early:**  
   Stop the inner loop early if the difference exceeds `k`.

---

## Code Implementation

```java
class Solution {
    public int findPairs(int[] nums, int k) {
        int n = nums.length;
        int count = 0;

        // Step 1: Sort the array
        Arrays.sort(nums);

        // Step 2: Iterate through the array
        for (int i = 0; i < n; i++) {
            // Skip duplicates for the current number
            if (i > 0 && nums[i] == nums[i - 1]) continue;

            // Find the target value nums[i] + k in the remaining array
            for (int j = i + 1; j < n; j++) {
                if (nums[j] - nums[i] == k) {
                    count++;
                    break; // Break once a valid pair is found
                } else if (nums[j] - nums[i] > k) {
                    break; // Stop early if the difference exceeds k
                }
            }
        }

        // Step 3: Return the total count of unique pairs
        return count;
    }
}
