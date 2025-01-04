# Image Smoother
[Problem Link](https://leetcode.com/problems/image-smoother/)

An image smoother is a filter of the size 3 x 3 that can be applied to each cell of an image by rounding down the average of the cell and the eight surrounding cells. If one or more of the surrounding cells is not present, we do not consider it in the average.

Given an `m x n` integer matrix `img` representing the grayscale of an image, return the image after applying the smoother on each cell of it.

### Input:
```img = [[1,1,1],[1,0,1],[1,1,1]]```

### Output:
```[[0,0,0],[0,0,0],[0,0,0]]```

### Explanation:
- For the points (0,0), (0,2), (2,0), (2,2): floor(3/4) = floor(0.75) = 0
- For the points (0,1), (1,0), (1,2), (2,1): floor(5/6) = floor(0.83333333) = 0
- For the point (1,1): floor(8/9) = floor(0.88888889) = 0

### Input:
- `img = [[100,200,100],[200,50,200],[100,200,100]]`

### Output:
```[[137,141,137],[141,138,141],[137,141,137]]```

### Explanation:
- For the points (0,0), (0,2), (2,0), (2,2): floor((100+200+200+50)/4) = floor(137.5) = 137
- For the points (0,1), (1,0), (1,2), (2,1): floor((200+200+50+200+100+100)/6) = floor(141.666667) = 141
- For the point (1,1): floor((50+200+200+200+200+100+100+100+100)/9) = floor(138.888889) = 138

### Solution
```java
class Solution {
    public int[][] imageSmoother(int[][] img) {
        int m = img.length;
        int n = img[0].length;
        int[][] ans = new int[m][n];

        int dx[] = {-1,-1,-1,0,0,1,1,1};
        int dy[] = {1,0,-1,1,-1,0,-1,1};
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int sum = img[i][j]; // Start with current cell
                int count = 1;
                for (int d = 0; d < 8; d++) {
                    int newi = i + dx[d];
                    int newj = j + dy[d];
                    if (newi < m && newi >= 0 && newj < n && newj >= 0) {
                        sum += img[newi][newj];
                        count++;
                    }
                }
                ans[i][j] = sum / count;
            }
        }
        return ans;
    }
}
```

### Accepted
![image](https://github.com/user-attachments/assets/ee2bdbec-f045-401d-b068-0a5b98f9d009)

