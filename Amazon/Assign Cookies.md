# Assign Cookies to Maximize Content Children
[Problem Link](https://leetcode.com/problems/assign-cookies/)

## Problem Description

You are tasked with assigning cookies to children such that each child gets at most one cookie. Each child `i` has a greed factor `g[i]`, which represents the minimum size of a cookie that will make the child content. Each cookie `j` has a size `s[j]`.

A cookie `j` can be assigned to a child `i` if `s[j] >= g[i]`. The goal is to maximize the number of content children and output this maximum number.

---

### Example 1:
**Input:**
```text
g = [1, 2, 3]
s = [1, 1]
```

**Output:**
```text
1
```

**Explanation:**
- Greed factors: [1, 2, 3]
- Cookie sizes: [1, 1]
- Only one child (greed factor = 1) can be made content using one of the cookies of size 1.

---

### Example 2:
**Input:**
```text
g = [1, 2]
s = [1, 2, 3]
```

**Output:**
```text
2
```

**Explanation:**
- Greed factors: [1, 2]
- Cookie sizes: [1, 2, 3]
- Both children can be made content since there are cookies of size 1 and 2 available.

---

## Solution

```java
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        int count = 0;
        Arrays.sort(g); // Sort greed factors of children
        Arrays.sort(s); // Sort sizes of cookies
        int i = 0;
        for (int j = 0; i < g.length && j < s.length; j++) {
            if (s[j] >= g[i]) { // If the cookie satisfies the child's greed factor
                count++;       // Increment the count of content children
                i++;           // Move to the next child
            }
        }
        return count;
    }
}
```
---

## Time Complexity:
- Sorting the arrays takes `O(n log n)` where `n` is the size of the larger array (`g` or `s`).
- Iterating through the arrays takes `O(n)`.
- Overall complexity: **`O(n log n)`**.

## Space Complexity:
- The space complexity is **`O(1)`**, as we only use a constant amount of extra space.

---

## Accepted Solution
![image](https://github.com/user-attachments/assets/8ecd39e2-c03b-4cab-b50c-cc288ec828b3)
