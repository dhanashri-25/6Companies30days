# 845. Longest Mountain in Array
[Problem Link](https://leetcode.com/problems/longest-mountain-in-array/)

## Question

You may recall that an array `arr` is a mountain array if and only if:

- `arr.length >= 3`
- There exists some index `i` (0-indexed) with `0 < i < arr.length - 1` such that:
  - `arr[0] < arr[1] < ... < arr[i - 1] < arr[i]`
  - `arr[i] > arr[i + 1] > ... > arr[arr.length - 1]`

Given an integer array `arr`, return the length of the longest subarray, which is a mountain. Return 0 if there is no mountain subarray.

### Example 1:
**Input**: `arr = [2,1,4,7,3,2,5]`  
**Output**: `5`  
**Explanation**: The largest mountain is `[1,4,7,3,2]` which has length 5.

### Example 2:
**Input**: `arr = [2,2,2]`  
**Output**: `0`  
**Explanation**: There is no mountain.

## Solution

```java
class Solution {
    public int longestMountain(int[] arr) {
        int maxlen = 0;
        int n = arr.length;
        
        // Iterate through the array to find peaks
        for (int i = 1; i < arr.length - 1; i++) {
            if (arr[i - 1] < arr[i] && arr[i] > arr[i + 1]) {
                // Step 1: Check for peak
                int left = i;
                while (left > 0 && arr[left - 1] < arr[left]) {
                    left--;  // Move left to the start of the mountain
                }
                
                // Step 2: Check right side of mountain
                int right = i + 1;
                while (right < n - 1 && arr[right] > arr[right + 1]) {
                    right++;  // Move right to the end of the mountain
                }
                
                // Step 3: Calculate mountain length
                int len = right - left + 1;
                maxlen = Math.max(maxlen, len);  // Update maximum length
            }
        }
        return maxlen;  // Return the length of the longest mountain
    }
}
```

### Time Complexity:
- **O(n)**: We iterate through the array once to find the peaks and expand left and right, where `n` is the length of the array.

### Space Complexity:
- **O(1)**: We only use a few integer variables to store lengths and indexes, so the space complexity is constant.

### Accepted Solution: