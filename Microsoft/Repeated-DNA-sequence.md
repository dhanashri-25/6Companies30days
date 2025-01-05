# 187. Repeated DNA Sequences
[Problem link](https://leetcode.com/problems/repeated-dna-sequences/)

The DNA sequence is composed of a series of nucleotides abbreviated as 'A', 'C', 'G', and 'T'. 

For example, "ACGAATTCCG" is a DNA sequence.  
When studying DNA, it is useful to identify repeated sequences within the DNA.

Given a string `s` that represents a DNA sequence, return all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule. You may return the answer in any order.

### Example 1:
**Input:** `s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"`  
**Output:** `["AAAAACCCCC", "CCCCCAAAAA"]`

### Example 2:
**Input:** `s = "AAAAAAAAAAAAA"`  
**Output:** `["AAAAAAAAAA"]`

### Solution

```java
class Solution {
    public List<String> findRepeatedDnaSequences(String s) {
        List<String> ans = new ArrayList<>();
        HashMap<String, Integer> mp = new HashMap<>();
        if (s.length() < 10) return ans;
        
        for (int i = 0; i <= s.length() - 10; i++) {
            String sub = s.substring(i, i + 10);
            mp.put(sub, mp.getOrDefault(sub, 0) + 1);
        }
        
        for (String str : mp.keySet()) {
            if (mp.get(str) > 1) {
                ans.add(str);
            }
        }
        
        return ans;
    }
}
```