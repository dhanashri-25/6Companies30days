# Find the Winner of the Circular Game
[Problem Link](https://leetcode.com/problems/find-the-winner-of-the-circular-game/)

There are `n` friends that are playing a game. The friends are sitting in a circle and are numbered from 1 to `n` in clockwise order. The rules of the game are as follows:

- Start at the 1st friend.
- Count the next `k` friends in the clockwise direction, including the friend you started at. The counting wraps around the circle and may count some friends more than once.
- The last friend you counted leaves the circle and loses the game.
- If there is still more than one friend in the circle, go back to step 2 starting from the friend immediately clockwise of the friend who just lost and repeat.
- Else, the last friend in the circle wins the game.

### Input:
```n = 5, k = 2```

### Output:
```3```

### Explanation:
Here are the steps of the game:
1) Start at friend 1.
2) Count 2 friends clockwise, which are friends 1 and 2.
3) Friend 2 leaves the circle. Next start is friend 3.
4) Count 2 friends clockwise, which are friends 3 and 4.
5) Friend 4 leaves the circle. Next start is friend 5.
6) Count 2 friends clockwise, which are friends 5 and 1.
7) Friend 1 leaves the circle. Next start is friend 3.
8) Count 2 friends clockwise, which are friends 3 and 5.
9) Friend 5 leaves the circle. Only friend 3 is left, so they are the winner.

### Solution
```java
class Solution {
    public int findTheWinner(int n, int k) {
        Queue<Integer> q = new LinkedList<>();
        for (int i = 1; i <= n; i++) {
            q.add(i);
        }
        while (q.size() > 1) {
            for (int i = 1; i < k; i++) {
                q.add(q.remove());
            }
            q.remove(); // Remove kth friend
        }
        return q.remove();
    }
}
```

### Accepted
![image](https://github.com/user-attachments/assets/d59c8a18-ca20-4f2e-8d01-2990066c0875)


