# 718. Maximum Length of Repeated Subarray

## Problem Link
[LeetCode Problem 718](https://leetcode.com/problems/maximum-length-of-repeated-subarray/)

## Problem Description

Given two integer arrays `nums1` and `nums2`, return the maximum length of a subarray that appears in both arrays.

## Example 1:

**Input:**
```java
nums1 = [1,2,3,2,1], nums2 = [3,2,1,4,7]
```

**Output:**
```java
3
```

**Explanation:**
The repeated subarray with maximum length is `[3,2,1]`.

## Solution:

```java
class Solution {
    public int findLength(int[] nums1, int[] nums2) {
        int n = nums1.length, m = nums2.length;
        int[][] dp = new int[n+1][m+1]; // Memoization table
        int maxlength = 0;

        // Iterate through both arrays and compare elements
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                // If elements match, increment the count of common subarray
                if (nums1[i-1] == nums2[j-1]) {
                    dp[i][j] = dp[i-1][j-1] + 1;
                    maxlength = Math.max(maxlength, dp[i][j]);
                } else {
                    dp[i][j] = 0;
                }
            }
        }
        return maxlength;
    }
}
```

### Explanation of DP Table:
- `dp[i][j]` represents the length of the longest common subarray that ends at `nums1[i-1]` and `nums2[j-1]`.
- When elements `nums1[i-1]` and `nums2[j-1]` match, we add 1 to the previous value of `dp[i-1][j-1]`, which keeps track of the length of the common subarray.
- If they don't match, we reset `dp[i][j]` to 0.

### Time Complexity:
- The time complexity is `O(n * m)` where `n` is the length of `nums1` and `m` is the length of `nums2` because we are using a nested loop to fill the DP table.

### Space Complexity:
- The space complexity is `O(n * m)` for the `dp` table.

