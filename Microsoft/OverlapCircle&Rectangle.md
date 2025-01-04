# Circle and Rectangle Overlapping
[Problem Link](https://leetcode.com/problems/circle-and-rectangle-overlapping/)
You are given a circle represented as (radius, xCenter, yCenter) and an axis-aligned rectangle represented as (x1, y1, x2, y2), where (x1, y1) are the coordinates of the bottom-left corner, and (x2, y2) are the coordinates of the top-right corner of the rectangle.

Return true if the circle and rectangle are overlapped, otherwise return false. In other words, check if there is any point (xi, yi) that belongs to the circle and the rectangle at the same time.

### Input:
```radius = 1, xCenter = 0, yCenter = 0, x1 = 1, y1 = -1, x2 = 3, y2 = 1```

### Output:
```true```

### Solution
```java
class Solution {
    public boolean checkOverlap(int radius, int xCenter, int yCenter, int x1, int y1, int x2, int y2) {
        int nearestx = Math.max(x1, Math.min(x2, xCenter));
        int nearesty = Math.max(y1, Math.min(y2, yCenter));
        int distx = xCenter - nearestx;
        int disty = yCenter - nearesty;
        return radius * radius >= distx * distx + disty * disty;
    }
}
```

### Accepted
![image](https://github.com/user-attachments/assets/9b2b268d-860b-44a6-a581-4acfb4bc83ec)
