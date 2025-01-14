# Match Nuts and Bolts Efficiently
[Problem Link](https://practice.geeksforgeeks.org/problems/match-nuts-and-bolts/0)

## Problem Description

You are given a set of `n` nuts and bolts. There is a one-to-one mapping between the nuts and bolts. You need to match each nut with its corresponding bolt efficiently. The following constraints apply:
1. Nuts can only be compared with bolts, and bolts can only be compared with nuts.
2. Comparison between two nuts or two bolts is not allowed.

The matching should follow a specific order:  
**{!, #, $, %, &, *, ?, @, ^}**

### Input:
- **n:** Integer denoting the number of nuts and bolts.
- **nuts[]:** Array of characters representing the nuts.
- **bolts[]:** Array of characters representing the bolts.

### Output:
- Matched nuts and bolts, sorted in the specified order.

---

### Example 1:
**Input:**
```text
n = 5
nuts[] = {@, %, $, #, ^}
bolts[] = {%, @, #, $, ^}
```

**Output:**
```text
# $ % @ ^
# $ % @ ^
```

**Explanation:** Both arrays are sorted in the required order.

---

### Example 2:
**Input:**
```text
n = 9
nuts[] = {^, &, %, @, #, *, $, ?, !}
bolts[] = {?, #, @, %, &, *, $, ^, !}
```

**Output:**
```text
! # $ % & * ? @ ^
! # $ % & * ? @ ^
```

**Explanation:** Both arrays are sorted in the required order.

---

### Code:
```java
import java.util.*;

class Solution {
    public void matchPairs(char[] nuts, char[] bolts, int n) {
        // Define the required order
        String order = "!#$%&*?@^";
        Map<Character, Integer> priorityMap = new HashMap<>();

        // Create a priority map for characters
        for (int i = 0; i < order.length(); i++) {
            priorityMap.put(order.charAt(i), i);
        }

        // Custom comparator based on the priority map
        Comparator<Character> comparator = (a, b) -> priorityMap.get(a) - priorityMap.get(b);

        // Sort nuts and bolts arrays
        Arrays.sort(nuts, comparator);
        Arrays.sort(bolts, comparator);
    }
}
```

---

## Time Complexity:
- Sorting both arrays takes **`O(n log n)`**, where `n` is the number of nuts (or bolts).
- Overall complexity: **`O(n log n)`**.

## Space Complexity:
- The space complexity for the priority map is **`O(1)`** since the order is fixed.
- The sorting space complexity is **`O(log n)`** due to the internal sorting algorithm.

---

## Accepted Solution