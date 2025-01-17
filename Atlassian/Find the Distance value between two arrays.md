# 1385. Find the Distance Value Between Two Arrays

## Problem Link
[LeetCode Problem 1385](https://leetcode.com/problems/find-the-distance-value-between-two-arrays/)

## Problem Description

Given two integer arrays `arr1` and `arr2`, and an integer `d`, return the distance value between the two arrays. 

The distance value is defined as the number of elements `arr1[i]` such that there is not any element `arr2[j]` where `|arr1[i] - arr2[j]| <= d`.

## Example 1:

**Input:**
```java
arr1 = [4,5,8], arr2 = [10,9,1,8], d = 2
```

**Output:**
```java
2
```

**Explanation:**
- For `arr1[0]=4`, we have:
  - |4-10| = 6 > d = 2
  - |4-9| = 5 > d = 2
  - |4-1| = 3 > d = 2
  - |4-8| = 4 > d = 2
- For `arr1[1]=5`, we have:
  - |5-10| = 5 > d = 2
  - |5-9| = 4 > d = 2
  - |5-1| = 4 > d = 2
  - |5-8| = 3 > d = 2
- For `arr1[2]=8`, we have:
  - |8-10| = 2 <= d = 2
  - |8-9| = 1 <= d = 2
  - |8-1| = 7 > d = 2
  - |8-8| = 0 <= d = 2

Therefore, the distance value is `2`.

## Solution:

```java
class Solution {
    public int findTheDistanceValue(int[] arr1, int[] arr2, int d) {
        int count = 0;
        for (int i = 0; i < arr1.length; i++) {
            boolean isValid = true;
            for (int j = 0; j < arr2.length; j++) {
                if (Math.abs(arr1[i] - arr2[j]) <= d) {
                    isValid = false;
                    break;
                }
            }
            if (isValid) {
                count++;
            }
        }
        return count;
    }
}
```

### Time Complexity:
- The time complexity is `O(n * m)` where `n` is the length of `arr1` and `m` is the length of `arr2`, since we are iterating over all elements in both arrays.

### Space Complexity:
- The space complexity is `O(1)` since no extra space is used apart from the input arrays and a few variables.