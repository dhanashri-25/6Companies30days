# 994. Rotting Oranges

[Leetcode Problem Link](https://leetcode.com/problems/rotting-oranges/)

## Problem Description

You are given an `m x n` grid where each cell can have one of three values:

- `0` representing an empty cell,
- `1` representing a fresh orange, or
- `2` representing a rotten orange.

Every minute, any fresh orange that is 4-directionally adjacent to a rotten orange becomes rotten.

Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return `-1`.

### Example 1:

**Input:**
```plaintext
grid = [[2,1,1],[1,1,0],[0,1,1]]
```

**Output:**
```plaintext
4
```

### Example 2:

**Input:**
```plaintext
grid = [[2,1,1],[0,1,1],[1,0,1]]
```

**Output:**
```plaintext
-1
```

**Explanation:**
The orange in the bottom right corner (`grid[2][2]`) will never rot because it is not adjacent to any rotten orange.

---

## Solution

The problem can be solved using **Breadth-First Search (BFS)**, where rotten oranges are treated as the starting points, and the BFS explores their neighbors (fresh oranges) to rot them minute by minute.

### Implementation

```java
import java.util.*;

class Solution {
    public int orangesRotting(int[][] grid) {
        if (grid == null || grid.length == 0) return 0;

        int m = grid.length;
        int n = grid[0].length;
        int[][] visited = new int[m][n];
        Queue<int[]> q = new LinkedList<>();
        int count_fresh = 0;

        // Add all rotten oranges to the queue and count fresh oranges
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 2) {
                    q.add(new int[]{i, j});
                    visited[i][j] = 1;
                } else if (grid[i][j] == 1) {
                    count_fresh++;
                }
            }
        }

        // Edge cases
        if (count_fresh == 0) return 0; // No fresh oranges
        if (q.isEmpty()) return -1; // No rotten oranges

        int minutes = -1;
        int[] dx = {-1, 1, 0, 0};
        int[] dy = {0, 0, -1, 1};

        // BFS to rot the oranges
        while (!q.isEmpty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                int[] elem = q.poll();
                int x = elem[0], y = elem[1];

                // Explore neighbors
                for (int j = 0; j < 4; j++) {
                    int newx = x + dx[j];
                    int newy = y + dy[j];

                    // Check if the new position is valid and contains a fresh orange
                    if (newx >= 0 && newx < m && newy >= 0 && newy < n && visited[newx][newy] == 0 && grid[newx][newy] == 1) {
                        grid[newx][newy] = 2; // Rot the orange
                        visited[newx][newy] = 1; // Mark as visited
                        count_fresh--;
                        q.add(new int[]{newx, newy});
                    }
                }
            }
            minutes++; // Increment time after processing all neighbors
        }

        // If there are still fresh oranges left, return -1
        return count_fresh == 0 ? minutes : -1;
    }
}
```

---

## Explanation

### Steps:
1. **Initialization**:
   - Count all fresh oranges and add all rotten oranges to the queue.
   - Use a `visited` matrix to track which cells have been processed.

2. **Breadth-First Search (BFS)**:
   - For each rotten orange, attempt to rot its 4-directional neighbors (up, down, left, right).
   - If a fresh orange is adjacent, rot it, mark it as visited, and add it to the queue.

3. **Time Calculation**:
   - Increment the time counter after processing all neighbors of the current level.

4. **Final Check**:
   - If all fresh oranges are rotted (`count_fresh == 0`), return the total time taken.
   - Otherwise, return `-1` if some fresh oranges remain isolated.

---

## Complexity Analysis

- **Time Complexity**: O(m × n)
  - Each cell is processed once, either as part of the initial grid scan or during the BFS.

- **Space Complexity**: O(m × n)
  - The `visited` array and the queue can each hold up to `m × n` elements in the worst case.

---
   
