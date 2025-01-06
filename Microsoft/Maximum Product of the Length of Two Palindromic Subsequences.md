# Maximum Product of the Length of Two Palindromic Subsequences
[Problem Link](https://leetcode.com/problems/maximum-product-of-the-length-of-two-palindromic-subsequences/)

Given a string `s`, find two disjoint palindromic subsequences of `s` such that the product of their lengths is maximized. The two subsequences are disjoint if they do not both pick a character at the same index.

A subsequence is a string that can be derived from another string by deleting some or no characters without changing the order of the remaining characters. A string is palindromic if it reads the same forward and backward.

Return the maximum possible product of the lengths of the two palindromic subsequences.

### Input:
```s = "leetcodecom"```

### Output:
```9```

### Solution
```java
class Solution {
    public int maxProduct(String s) {
        int n = s.length();
        int maxProduct = 0;
        for (int mask = 1; mask < (1 << n); mask++) {
            StringBuilder s1 = new StringBuilder();
            StringBuilder s2 = new StringBuilder();
            for (int i = 0; i < n; i++) {
                if ((mask & (1 << i)) != 0) {
                    s1.append(s.charAt(i));
                } else {
                    s2.append(s.charAt(i));
                }
            }
            int len1 = longestPalindromeSubseq(s1.toString());
            int len2 = longestPalindromeSubseq(s2.toString());
            maxProduct = Math.max(maxProduct, len1 * len2);
        }
        return maxProduct;
    }

    public int func(int m, int n, String s1, String s2, int[][] dp) {
        if (m == 0 || n == 0) return 0;
        if (dp[m][n] != -1) return dp[m][n];
        if (s1.charAt(m - 1) == s2.charAt(n - 1)) {
            dp[m][n] = 1 + func(m - 1, n - 1, s1, s2, dp);
        } else {
            dp[m][n] = Math.max(func(m - 1, n, s1, s2, dp), func(m, n - 1, s1, s2, dp));
        }
        return dp[m][n];
    }

    public int longestPalindromeSubseq(String s) {
        int m = s.length();
        StringBuilder sb = new StringBuilder(s);
        String s2 = sb.reverse().toString();
        int[][] dp = new int[m + 1][m + 1];
        for (int[] row : dp) {
            Arrays.fill(row, -1);
        }
        return func(m, m, s, s2, dp);
    }
}
```

### Accepted
![image](https://github.com/user-attachments/assets/fa5fa633-984f-4ccb-b6e5-b6ca390433be)
