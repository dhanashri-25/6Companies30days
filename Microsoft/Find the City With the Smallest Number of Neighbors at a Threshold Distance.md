# Find the City With the Smallest Number of Neighbors at a Threshold Distance
[Problem Link](https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/)

There are `n` cities numbered from `0` to `n-1`. Given the array `edges` where `edges[i] = [fromi, toi, weighti]` represents a bidirectional and weighted edge between cities `fromi` and `toi`, and given the integer `distanceThreshold`.

Return the city with the smallest number of cities that are reachable through some path and whose distance is at most `distanceThreshold`. If there are multiple such cities, return the city with the greatest number.

Notice that the distance of a path connecting cities `i` and `j` is equal to the sum of the edges' weights along that path.

### Input:
```n = 4, edges = [[0,1,3],[1,2,1],[1,3,4],[2,3,1]], distanceThreshold = 4```

### Output:
```3```

### Solution
```java
class Solution {
    public int findTheCity(int n, int[][] edges, int distanceThreshold) {
        int[][] dist = new int[n][n];
        
        // Initialize distance matrix
        for (int i = 0; i < n; i++) {
            Arrays.fill(dist[i], Integer.MAX_VALUE);
            dist[i][i] = 0;
        }
        
        // Fill the distance matrix with edge weights
        for (int[] edge : edges) {
            dist[edge[0]][edge[1]] = edge[2];
            dist[edge[1]][edge[0]] = edge[2];
        }

        // Floyd-Warshall algorithm to compute all pairs shortest paths
        for (int k = 0; k < n; k++) {
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    if (dist[i][k] != Integer.MAX_VALUE && dist[k][j] != Integer.MAX_VALUE) {
                        dist[i][j] = Math.min(dist[i][j], dist[i][k] + dist[k][j]);
                    }
                }
            }
        }

        // Find the city with the smallest number of neighbors within the distance threshold
        int minNeighbors = n;
        int cityWithSmallestNeighbors = -1;

        for (int i = 0; i < n; i++) {
            int neighbors = 0;
            for (int j = 0; j < n; j++) {
                if (dist[i][j] <= distanceThreshold) {
                    neighbors++;
                }
            }
            if (neighbors <= minNeighbors) {
                minNeighbors = neighbors;
                cityWithSmallestNeighbors = i;
            }
        }

        return cityWithSmallestNeighbors;
    }
}
```

### Accepted
![image](https://github.com/user-attachments/assets/1e486d6b-267a-46f3-86d8-80b99ca9a28d)

