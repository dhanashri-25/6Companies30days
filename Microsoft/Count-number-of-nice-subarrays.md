### Problem: Count Number of Nice Subarrays
[Problem Link](https://leetcode.com/problems/count-number-of-nice-subarrays/description/)

Given an array of integers `nums` and an integer `k`, a continuous subarray is called **nice** if there are exactly `k` odd numbers in it. The task is to return the number of **nice** subarrays.

**Input:**
```java
nums = [1, 1, 2, 1, 1], k = 3
```

**Output:**
```java
2
```

**Explanation:**
The only subarrays with exactly 3 odd numbers are:
- [1, 1, 2, 1]
- [1, 2, 1, 1]

**Example 2:**

**Input:**
```java
nums = [2, 4, 6], k = 1
```

**Output:**
```java
0
```

**Explanation:**
There are no odd numbers in the array, so the answer is 0.

**Example 3:**

**Input:**
```java
nums = [2, 2, 2, 1, 2, 2, 1, 2, 2, 2], k = 2
```

**Output:**
```java
16
```

---

### Solution Explanation

The approach to solving this problem is to utilize a **sliding window** technique, which is efficient in counting subarrays based on a given condition. 

To achieve this, we will solve the problem using a helper function that calculates the number of subarrays with **at most** `k` odd numbers, and then use this to compute the number of subarrays with **exactly** `k` odd numbers.

#### Steps:
1. **Convert the Problem to Subarrays with At Most `k` Odd Numbers:**
   - We can convert all even numbers to 0 and odd numbers to 1.
   - We then count the number of subarrays that contain **at most** `k` odd numbers using a sliding window.

2. **Calculate the Number of Subarrays with Exactly `k` Odd Numbers:**
   - The number of subarrays with **exactly** `k` odd numbers is the difference between:
     - The number of subarrays with **at most** `k` odd numbers.
     - The number of subarrays with **at most** `k-1` odd numbers.

---

### Code

```java
class Solution {
    // Helper function to count subarrays with at most k odd numbers
    public int lessthanOrEqualTo(int[] nums, int k) {
        int l = 0, count = 0, sum = 0;
        for (int r = 0; r < nums.length; r++) {
            sum += nums[r] % 2;  // Convert odd numbers to 1 and even numbers to 0
            while (sum > k) {  // Shrink the window if the count of odd numbers exceeds k
                sum -= nums[l] % 2;
                l++;
            }
            count += (r - l + 1);  // Count the valid subarrays ending at r
        }
        return count;
    }

    // Main function to calculate the number of subarrays with exactly k odd numbers
    public int numberOfSubarrays(int[] nums, int k) {
        return lessthanOrEqualTo(nums, k) - lessthanOrEqualTo(nums, k - 1);
    }
}
```

---

### Time Complexity

- The time complexity of the solution is **O(n)**, where `n` is the length of the input array `nums`. The sliding window technique ensures that each element is processed at most twice (once when expanding the window and once when contracting it).

---

### Explanation in Simple Terms:

1. **Convert the Problem:** Think of every odd number as 1 and every even number as 0. Now, we need to count how many subarrays have **at most** `k` ones (odd numbers).

2. **Sliding Window Approach:** 
   - We maintain a window of elements that contains at most `k` odd numbers. If the window exceeds `k` odd numbers, we shrink it from the left side.
   - The count of valid subarrays ending at each position `r` is calculated as `(r - l + 1)`.

3. **Calculate Subarrays with Exactly `k` Odd Numbers:**
   - Subarrays with exactly `k` odd numbers can be found by subtracting the count of subarrays with **at most** `k-1` odd numbers from the count of subarrays with **at most** `k` odd numbers.

This technique efficiently counts the subarrays while maintaining a time complexity of O(n), which is optimal for large input sizes.

