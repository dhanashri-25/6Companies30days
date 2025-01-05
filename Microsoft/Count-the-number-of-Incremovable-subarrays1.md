### 2970. Count the Number of Incremovable Subarrays I
[Problem link](https://leetcode.com/problems/count-the-number-of-incremovable-subarrays-i/)

You are given a 0-indexed array of positive integers `nums`.

A subarray of `nums` is called **incremovable** if `nums` becomes strictly increasing on removing the subarray. For example, the subarray `[3, 4]` is an incremovable subarray of `[5, 3, 4, 6, 7]` because removing this subarray changes the array `[5, 3, 4, 6, 7]` to `[5, 6, 7]`, which is strictly increasing.

Return the total number of incremovable subarrays of `nums`.

### Example 1:
**Input:** `nums = [1,2,3,4]`  
**Output:** `10`  
**Explanation:** The 10 incremovable subarrays are: `[1]`, `[2]`, `[3]`, `[4]`, `[1,2]`, `[2,3]`, `[3,4]`, `[1,2,3]`, `[2,3,4]`, and `[1,2,3,4]` because removing any one of these subarrays makes `nums` strictly increasing.

### Example 2:
**Input:** `nums = [6,5,7,8]`  
**Output:** `7`  
**Explanation:** The 7 incremovable subarrays are: `[5]`, `[6]`, `[5,7]`, `[6,5]`, `[5,7,8]`, `[6,5,7]`, and `[6,5,7,8]`.

### Example 3:
**Input:** `nums = [8,7,6,6]`  
**Output:** `3`  
**Explanation:** The 3 incremovable subarrays are: `[8,7,6]`, `[7,6,6]`, and `[8,7,6,6]`.  

### Solution

```java
class Solution {
    public boolean countSubarrays(int [] nums, int st, int end) {
        // Left part: Check if all elements before 'st' are strictly increasing
        for (int i = 1; i < st; i++) {
            if (nums[i] <= nums[i - 1]) {
                return false;
            }
        }
        // Check if the elements adjacent to the subarray maintain strictly increasing property
        if (st > 0 && end < nums.length - 1 && nums[st - 1] >= nums[end + 1]) {
            return false;
        }
        // Right part: Check if all elements after 'end' are strictly increasing
        for (int i = end + 2; i < nums.length; i++) {
            if (nums[i] <= nums[i - 1]) {
                return false;
            }
        }
        return true;
    }

    public int incremovableSubarrayCount(int[] nums) {
        int n = nums.length;
        int count = 0;
        // Loop through all possible subarrays and count incremovable subarrays
        for (int st = 0; st < n; st++) {
            for (int end = st; end < n; end++) {
                if (countSubarrays(nums, st, end)) {
                    count++;
                }
            }
        }
        return count;
    }
}
```