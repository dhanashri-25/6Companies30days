# 324. Wiggle Sort II

[Problem Link](https://leetcode.com/problems/wiggle-sort-ii/)

Given an integer array `nums`, reorder it such that `nums[0] < nums[1] > nums[2] < nums[3]....`

You may assume the input array always has a valid answer.

### Example 1:

**Input:**

```plaintext
nums = [1,5,1,1,6,4]
```

**Output:**

```plaintext
[1,6,1,5,1,4]
```

**Explanation:**
`[1,4,1,5,1,6]` is also accepted.

### Example 2:

**Input:**

```plaintext
nums = [1,3,2,2,3,1]
```

**Output:**

```plaintext
[2,3,1,3,1,2]
```

### Solution

```java
class Solution {
    public void wiggleSort(int[] nums) {
        Arrays.sort(nums);
        int[] ans = new int[nums.length];
        int n = nums.length;
        int i = 1, j = nums.length - 1;

        // Fill even places
        while (i < n) {
            ans[i] = nums[j];
            i += 2;
            j--;
        }

        // Fill odd places
        i = 0;
        while (i < n) {
            ans[i] = nums[j];
            i += 2;
            j--;
        }

        for (int x = 0; x < nums.length; x++) {
            nums[x] = ans[x];
        }
    }
}
```

---
