# 825. Friends Of Appropriate Ages

## Problem Link
[LeetCode Problem 825](https://leetcode.com/problems/friends-of-appropriate-ages/)

## Problem Description

There are `n` persons on a social media website. You are given an integer array `ages` where `ages[i]` is the age of the `i`-th person.

A person `x` will not send a friend request to a person `y` (where `x != y`) if any of the following conditions is true:

- `age[y] <= 0.5 * age[x] + 7`
- `age[y] > age[x]`
- `age[y] > 100 && age[x] < 100`

Otherwise, `x` will send a friend request to `y`.

Note that if `x` sends a request to `y`, `y` will not necessarily send a request to `x`. Also, a person will not send a friend request to themselves.

Return the total number of friend requests made.

## Example 1:

**Input:**
```java
ages = [16, 16]
```

**Output:**
```java
2
```

**Explanation:**
Two people friend request each other.

## Example 2:

**Input:**
```java
ages = [16, 17, 18]
```

**Output:**
```java
2
```

**Explanation:**
Friend requests are made:
- 17 -> 16
- 18 -> 17

## Solution:

```java
class Solution {
    public int numFriendRequests(int[] ages) {
        int[] arr = new int[121]; // Array to store the frequency of each age
        int ans = 0;
        
        // Count the frequency of each age
        for (int a : ages) {
            arr[a]++;
        }
        
        // Check for friend requests based on the given conditions
        for (int i = 1; i < 121; i++) {
            for (int j = 1; j < 121; j++) {
                int a = arr[i];
                int b = arr[j];
                if (j > 0.5 * i + 7 && i >= j && (j <= 100 || i >= 100)) {
                    // If person x (age i) can send a request to person y (age j)
                    ans += i == j ? a * b - a : a * b; // Avoid double-counting for the same person
                }
            }
        }
        
        return ans;
    }
}
```

### Time Complexity:
- The time complexity is `O(121 * 121)`, which is constant since 121 is a fixed value. Essentially, it's `O(1)` in terms of time complexity, but the nested loops iterate over the age range.

### Space Complexity:
- The space complexity is `O(121)`, as we use an array of size 121 to store the frequency of each age.

