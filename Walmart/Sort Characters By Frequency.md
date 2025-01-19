# 451. Sort Characters By Frequency

## Problem Link
[LeetCode Problem 451](https://leetcode.com/problems/sort-characters-by-frequency/)

## Problem Description

Given a string `s`, sort it in decreasing order based on the frequency of the characters. The frequency of a character is the number of times it appears in the string.

Return the sorted string. If there are multiple answers, return any of them.

---
#### Example 1:
**Input:**
```java
s = "tree"
```

**Output:**
```java
"eert"
```

**Explanation:**
- 'e' appears twice while 'r' and 't' both appear once.
- So 'e' must appear before both 'r' and 't'. Therefore `"eetr"` is also a valid answer.

#### Example 2:
**Input:**
```java
s = "cccaaa"
```

**Output:**
```java
"aaaccc"
```

**Explanation:**
- Both 'c' and 'a' appear three times, so both `"cccaaa"` and `"aaaccc"` are valid answers.
- Note that `"cacaca"` is incorrect, as the same characters must be grouped together.

#### Example 3:
**Input:**
```java
s = "Aabb"
```

**Output:**
```java
"bbAa"
```

**Explanation:**
- `"bbaA"` is also a valid answer, but `"Aabb"` is incorrect.
- Note that 'A' and 'a' are treated as two different characters.

---

## Solution:

```java
class Solution {
    public String frequencySort(String s) {
        // Step 1: Count the frequency of each character
        Map<Character, Integer> mp = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            mp.put(s.charAt(i), mp.getOrDefault(s.charAt(i), 0) + 1);
        }

        // Step 2: Create a list of unique characters from the string
        List<Character> anslist = new ArrayList<>(mp.keySet());

        // Step 3: Sort the characters by their frequency in descending order
        Collections.sort(anslist, (a, b) -> {
            return mp.get(b) - mp.get(a);
        });

        // Step 4: Build the result string
        StringBuilder sb = new StringBuilder();
        for (Character c : anslist) {
            for (int i = 0; i < mp.get(c); i++) {
                sb.append(c);
            }
        }

        return sb.toString();
    }
}
```

---

### Complexity Analysis:

#### Time Complexity:
1. Counting the frequency of characters: `O(n)`, where `n` is the length of the string.
2. Sorting the unique characters: `O(k log k)`, where `k` is the number of unique characters in the string.
3. Building the result string: `O(n)`.
- Overall: `O(n + k log k)`.

#### Space Complexity:
- `O(k)` for the `HashMap` and `List`, where `k` is the number of unique characters in the string.

---
