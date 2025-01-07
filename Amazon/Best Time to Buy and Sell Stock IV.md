# 188. Best Time to Buy and Sell Stock IV
[Problem Link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)

## Question

You are given an integer array `prices` where `prices[i]` is the price of a given stock on the ith day, and an integer `k`.

Find the maximum profit you can achieve. You may complete at most `k` transactions: i.e. you may buy at most `k` times and sell at most `k` times.

Note: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

### Example 1:
**Input**: `k = 2, prices = [2,4,1]`  
**Output**: `2`  
**Explanation**: Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4 - 2 = 2.

### Example 2:
**Input**: `k = 2, prices = [3,2,6,5,0,3]`  
**Output**: `7`  
**Explanation**: Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6 - 2 = 4. Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3 - 0 = 3.

## Solution

```java
class Solution {
    public int maxProfit(int k, int[] prices) {
        int n = prices.length;
        if (n == 0 || k == 0) return 0;
        int dp[][][] = new int[n + 1][2][k + 1];
        
        for (int i = n - 1; i >= 0; i--) {
            for (int buy = 0; buy <= 1; buy++) {
                for (int t = 1; t <= k; t++) {
                    if (buy == 1) {
                        dp[i][buy][t] = Math.max(dp[i + 1][1][t], dp[i + 1][0][t] - prices[i]);
                    } else {
                        dp[i][buy][t] = Math.max(dp[i + 1][0][t], dp[i + 1][1][t - 1] + prices[i]);
                    }
                }
            }
        }
        return dp[0][1][k];
    }
}
```

### Time Complexity:
- **O(n * k)**: We iterate through all the days and all possible transactions, where `n` is the length of the prices array and `k` is the maximum number of transactions allowed.

### Space Complexity:
- **O(n * k)**: We use a 3D dynamic programming array to store intermediate results for the given number of days, buy/sell states, and transaction counts.

### Accepted Solution: