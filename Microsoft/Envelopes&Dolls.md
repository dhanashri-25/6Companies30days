# 354. Russian Doll Envelopes

[Problem Link](https://leetcode.com/problems/russian-doll-envelopes/)

You are given a 2D array of integers `envelopes` where `envelopes[i] = [wi, hi]` represents the width and the height of an envelope.

One envelope can fit into another if and only if both the width and height of one envelope are greater than the other envelope's width and height.

Return the maximum number of envelopes you can Russian doll (i.e., put one inside the other).

Note: You cannot rotate an envelope.

### Example 1:

**Input:**

```plaintext
envelopes = [[5,4],[6,4],[6,7],[2,3]]
```

**Output:**

```plaintext
3
```

**Explanation:**
The maximum number of envelopes you can Russian doll is 3 ([2,3] => [5,4] => [6,7]).

### Example 2:

**Input:**

```plaintext
envelopes = [[1,1],[1,1],[1,1]]
```

**Output:**

```plaintext
1
```

### Solution

```java
class Solution {
    public int maxEnvelopes(int[][] envelopes) {
        int n = envelopes.length;

        // Step 1: Sort envelopes
        Arrays.sort(envelopes, (a, b) -> {
            if (a[0] == b[0]) {
                return b[1] - a[1]; // Sort by height descending if widths are equal
            } else {
                return a[0] - b[0]; // Sort by width ascending
            }
        });

        // Step 2: Extract heights for LIS
        int[] heights = new int[n];
        for (int i = 0; i < n; i++) {
            heights[i] = envelopes[i][1];
        }

        // Step 3: Find LIS using binary search
        return lengthOfLIS(heights);
    }

    private int lengthOfLIS(int[] nums) {
        List<Integer> lis = new ArrayList<>();

        for (int num : nums) {
            int index = binarySearch(lis, num);
            if (index == lis.size()) {
                lis.add(num); // Add to LIS if no larger element exists
            } else {
                lis.set(index, num); // Replace the element to maintain LIS
            }
        }

        return lis.size();
    }

    private int binarySearch(List<Integer> lis, int target) {
        int low = 0, high = lis.size() - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (lis.get(mid) < target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return low; // Position to insert the target
    }
}
```

---



