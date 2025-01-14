# Maximum of Subarrays of Size k
[Problem Link](https://www.geeksforgeeks.org/problems/maximum-of-all-subarrays-of-size-k3101/1)

## Problem Description

Given an array `arr[]` of integers and an integer `k`, your task is to find the maximum value for each contiguous subarray of size `k`. The output should be an array of maximum values corresponding to each contiguous subarray.

#### Example 1:
**Input:**
```text
arr[] = [1, 2, 3, 1, 4, 5, 2, 3, 6], k = 3
```

**Output:**
```text
[3, 3, 4, 5, 5, 5, 6]
```

**Explanation:**
- 1st contiguous subarray = [1 2 3], max = 3
- 2nd contiguous subarray = [2 3 1], max = 3
- 3rd contiguous subarray = [3 1 4], max = 4
- 4th contiguous subarray = [1 4 5], max = 5
- 5th contiguous subarray = [4 5 2], max = 5
- 6th contiguous subarray = [5 2 3], max = 5
- 7th contiguous subarray = [2 3 6], max = 6

## Solution

```java
class Solution {
    class Pair {
        int val;
        int index;
        
        Pair(int val, int index) {
            this.val = val;
            this.index = index;
        }
    }
    
    public ArrayList<Integer> max_of_subarrays(int arr[], int k) {
        ArrayList<Integer> ans = new ArrayList<>();
        PriorityQueue<Pair> q = new PriorityQueue<>((a, b) -> b.val - a.val);
        
        // Add first k elements to the queue
        for (int i = 0; i < k; i++) {
            q.add(new Pair(arr[i], i));
        }
        
        // Add the maximum of the first subarray to the answer
        ans.add(q.peek().val);
        
        // Process the rest of the array
        for (int i = k; i < arr.length; i++) {
            q.add(new Pair(arr[i], i));
            
            // Shrink the window by removing elements outside the range of the current subarray
            while (q.peek().index <= i - k) {
                q.poll();
            }
            
            // Add the maximum element of the current subarray to the answer
            ans.add(q.peek().val);
        }
        
        return ans;
    }
}
```

## Time Complexity:
- The time complexity of adding an element to the priority queue is `O(log k)`, and we do this for each element in the array.
- Hence, the total time complexity is `O(n log k)` where `n` is the number of elements in the array.

## Space Complexity:
- The space complexity is `O(k)` because we store at most `k` elements in the priority queue at any given time.
```
## Accepted Solution
