# 2461. Maximum Sum of Distinct Subarrays With Length K

[Problem Link](https://leetcode.com/problems/maximum-sum-of-distinct-subarrays-with-length-k/)

You are given an integer array `nums` and an integer `k`. Find the maximum subarray sum of all the subarrays of `nums` that meet the following conditions:

1. The length of the subarray is `k`, and
2. All the elements of the subarray are distinct.

Return the maximum subarray sum of all the subarrays that meet the conditions. If no subarray meets the conditions, return `0`.

A subarray is a contiguous non-empty sequence of elements within an array.

### Example 1:

**Input:**

```plaintext
nums = [1,5,4,2,9,9,9], k = 3
```

**Output:**

```plaintext
15
```

**Explanation:**
The subarrays of `nums` with length 3 are:

- `[1,5,4]` which meets the requirements and has a sum of 10.
- `[5,4,2]` which meets the requirements and has a sum of 11.
- `[4,2,9]` which meets the requirements and has a sum of 15.
- `[2,9,9]` which does not meet the requirements because the element 9 is repeated.
- `[9,9,9]` which does not meet the requirements because the element 9 is repeated.
  We return 15 because it is the maximum subarray sum of all the subarrays that meet the conditions.

### Example 2:

**Input:**

```plaintext
nums = [4,4,4], k = 3
```

**Output:**

```plaintext
0
```

**Explanation:**
The subarrays of `nums` with length 3 are:

- `[4,4,4]` which does not meet the requirements because the element 4 is repeated.
  We return 0 because no subarrays meet the conditions.

### Solution

```java
class Solution {
    public long maximumSubarraySum(int[] nums, int k) {
        long sum = 0, maxsum = 0;
        HashMap<Integer, Integer> mp = new HashMap<>();
        int l = 0, r = 0;

        while (r < nums.length) {
            mp.put(nums[r], mp.getOrDefault(nums[r], 0) + 1);
            sum += nums[r];

            if (r - l + 1 > k) {
                sum -= nums[l];
                mp.put(nums[l], mp.get(nums[l]) - 1);
                if (mp.get(nums[l]) == 0) mp.remove(nums[l]);
                l++;
            }

            if (r - l + 1 == k && mp.size() == k) {
                maxsum = Math.max(maxsum, sum);
            }

            r++;
        }

        return maxsum;
    }
}
```

---