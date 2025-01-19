# 139. Word Break

## Problem Link
[LeetCode Problem 139](https://leetcode.com/problems/word-break/)

## Problem Description

Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

Note that the same word in the dictionary may be reused multiple times in the segmentation.

### Example 1:

**Input:**
```java
s = "leetcode", wordDict = ["leet","code"]
```

**Output:**
```java
true
```

**Explanation:**
- Return `true` because `"leetcode"` can be segmented as `"leet code"`.

## Solution:

```java
class Solution { 
    public boolean wordBreak(String s, List<String> wordDict) {
        Set<String> wordset = new HashSet<>(wordDict); // Convert wordDict to a HashSet for faster lookup
        boolean[] dp = new boolean[s.length() + 1];
        dp[0] = true; // Base case: empty string can always be segmented

        // Iterate over the string
        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < i; j++) {
                // Check if substring from j to i exists in the set and dp[j] is true
                if (dp[j] && wordset.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }

        return dp[s.length()];
    }
}
```

### Explanation:
1. **HashSet for Fast Lookup:**
   - Convert `wordDict` into a `HashSet` (`wordset`) to optimize the search for substrings.
2. **Dynamic Programming Table (`dp`):**
   - `dp[i]` indicates whether the first `i` characters of the string `s` can be segmented into dictionary words.
   - Initialize `dp[0] = true`, as an empty string can always be segmented.
3. **Nested Loop:**
   - Outer loop iterates over all positions in the string.
   - Inner loop checks substrings ending at the current position `i` and starting at position `j`. If `dp[j]` is true and the substring from `j` to `i` is in `wordset`, mark `dp[i] = true` and break.

### Time Complexity:
- **Solution 1:** `O(n * max_len * k)` where `n` is the length of `s`, `max_len` is the length of the longest word in `wordDict`, and `k` is the size of `wordDict`.
- **Solution 2:** `O(n^2)` where `n` is the length of `s`. The worst case is if every prefix of `s` needs to be checked against `wordset`.

### Space Complexity:
- **Solution 1:** `O(n)`, for the `dp` array.
- **Solution 2:** `O(n + k)`, where `n` is the `dp` array and `k` is the size of the `HashSet`.

