# 2099. Find Subsequence of Length K With the Largest Sum
[problem link](https://leetcode.com/problems/find-subsequence-of-length-k-with-the-largest-sum/description/)

## Problem Description
You are given an integer array `nums` and an integer `k`. You want to find a subsequence of `nums` of length `k` that has the largest sum.

Return any such subsequence as an integer array of length `k`.

A **subsequence** is an array that can be derived from another array by deleting some or no elements without changing the order of the remaining elements.

---

## Examples

### Example 1:
**Input:**
```plaintext
nums = [2, 1, 3, 3], k = 2
```
**Output:**
```plaintext
[3, 3]
```
**Explanation:**
The subsequence has the largest sum of `3 + 3 = 6`.

### Example 2:
**Input:**
```plaintext
nums = [-1, -2, 3, 4], k = 3
```
**Output:**
```plaintext
[-1, 3, 4]
```
**Explanation:**
The subsequence has the largest sum of `-1 + 3 + 4 = 6`.

### Example 3:
**Input:**
```plaintext
nums = [3, 4, 3, 3], k = 2
```
**Output:**
```plaintext
[3, 4]
```
**Explanation:**
The subsequence has the largest sum of `3 + 4 = 7`. Another possible subsequence is `[4, 3]`.

---

## Solution

### Approach
1. Create a 2D array `elements` where each element is paired with its index.
2. Sort the `elements` array in descending order based on values.
3. Select the top `k` largest elements.
4. Sort the selected elements by their original indices to maintain the order.
5. Extract the values of the selected elements into the result array.
6. Return the result array as the subsequence.

---

### Code Implementation
```java
class Solution {
    public int[] maxSubsequence(int[] nums, int k) {
        // Step 1: Create a 2D array where each element is paired with its index
        int[][] elements = new int[nums.length][2];
        int n = nums.length;
        for (int i = 0; i < n; i++) {
            elements[i][0] = nums[i];  // Store the value
            elements[i][1] = i;       // Store the index
        }

        // Step 2: Sort the array in descending order based on values
        Arrays.sort(elements, (a, b) -> Integer.compare(b[0], a[0]));

        // Step 3: Select the top 'k' largest elements
        int[][] selected = Arrays.copyOfRange(elements, 0, k);

        // Step 4: Sort the selected elements by their original indices to maintain order
        Arrays.sort(selected, (a, b) -> Integer.compare(a[1], b[1]));

        // Step 5: Extract the values of the selected elements into the result array
        int[] result = new int[k];
        for (int i = 0; i < k; i++) {
            result[i] = selected[i][0];
        }

        // Step 6: Return the result array as the subsequence
        return result;
    }
}
```

---

### Example Walkthrough
#### Example 1:
- **Input:** `nums = [2, 1, 3, 3], k = 2`
- **Steps:**
  1. `elements = {{2, 0}, {1, 1}, {3, 2}, {3, 3}}`
  2. After sorting by value: `elements = {{3, 2}, {3, 3}, {2, 0}, {1, 1}}`
  3. Selecting top `k`: `selected = {{3, 2}, {3, 3}}`
  4. Sorting by index: `selected = {{3, 2}, {3, 3}}`
  5. Extracting values: `result = [3, 3]`
- **Output:** `[3, 3]`

#### Example 2:
- **Input:** `nums = [-1, -2, 3, 4], k = 3`
- **Steps:**
  1. `elements = {{-1, 0}, {-2, 1}, {3, 2}, {4, 3}}`
  2. After sorting by value: `elements = {{4, 3}, {3, 2}, {-1, 0}, {-2, 1}}`
  3. Selecting top `k`: `selected = {{4, 3}, {3, 2}, {-1, 0}}`
  4. Sorting by index: `selected = {{-1, 0}, {3, 2}, {4, 3}}`
  5. Extracting values: `result = [-1, 3, 4]`
- **Output:** `[-1, 3, 4]`

---

### Complexity Analysis
- **Time Complexity:**
  - Sorting `elements` by value: \(O(n \log n)\)
  - Sorting selected elements by index: \(O(k \log k)\)
  - Total: \(O(n \log n)\).
- **Space Complexity:** \(O(n)\) for the `elements` array.

---
