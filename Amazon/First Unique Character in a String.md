# 387. First Unique Character in a String
[Problem Link](https://leetcode.com/problems/first-unique-character-in-a-string/)

## Question

Given a string `s`, find the first non-repeating character in it and return its index. If it does not exist, return `-1`.

### Example 1:
**Input**: `s = "leetcode"`  
**Output**: `0`  
**Explanation**: The character 'l' at index 0 is the first character that does not occur at any other index.

### Example 2:
**Input**: `s = "loveleetcode"`  
**Output**: `2`

### Example 3:
**Input**: `s = "aabb"`  
**Output**: `-1`

## Solution

```java
class Solution {
    public int firstUniqChar(String s) {
        int freq[] = new int[26];  // Create a frequency array for lowercase English letters
        for (int i = 0; i < s.length(); i++) {
            freq[s.charAt(i) - 'a']++;  // Increment the frequency of the current character
        }
        
        for (int i = 0; i < s.length(); i++) {
            if (freq[s.charAt(i) - 'a'] == 1) {  // Check if the character occurs only once
                return i;  // Return the index of the first unique character
            }
        }
        return -1;  // Return -1 if no unique character is found
    }
}
```

### Time Complexity:
- **O(n)**: We traverse the string twice: once to count the frequency of each character, and once more to find the first unique character.

### Space Complexity:
- **O(1)**: The frequency array has a fixed size of 26, corresponding to the lowercase English letters, so the space complexity is constant.

### Accepted Solution:
