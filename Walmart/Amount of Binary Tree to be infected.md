# 2385. Amount of Time for Binary Tree to Be Infected

## Problem Link
[LeetCode Problem 2385](https://leetcode.com/problems/amount-of-time-for-binary-tree-to-be-infected/)

## Problem Description

You are given the root of a binary tree with unique values, and an integer `start`. At minute 0, an infection starts from the node with value `start`.

Each minute, a node becomes infected if:

- The node is currently uninfected.
- The node is adjacent to an infected node.

Return the number of minutes needed for the entire tree to be infected.

## Example 1:

**Input:**
```java
root = [1,5,3,null,4,10,6,9,2], start = 3
```

**Output:**
```java
4
```

**Explanation:**
The following nodes are infected during:
- Minute 0: Node 3
- Minute 1: Nodes 1, 10, and 6
- Minute 2: Node 5
- Minute 3: Node 4
- Minute 4: Nodes 9 and 2

It takes 4 minutes for the whole tree to be infected so we return 4.


## Solution:

```java
class Solution {
    public int amountOfTime(TreeNode root, int start) {
        Map<Integer, Set<Integer>> map = new HashMap<>(); // Creating graph to represent tree as undirected graph
        convert(root, 0, map); // Convert tree into graph
        int minute = 0;
        Queue<Integer> q = new LinkedList<>();
        q.add(start);
        Set<Integer> vis = new HashSet<>();
        vis.add(start);
        
        while (!q.isEmpty()) {
            int levelsize = q.size();
            while (levelsize > 0) {
                int curr = q.poll(); // Process the current node
                for (int num : map.get(curr)) {
                    if (!vis.contains(num)) {
                        vis.add(num);
                        q.add(num);
                    }
                }
                levelsize--;
            }
            minute++;
        }
        return minute - 1;
    }
    
    void convert(TreeNode curr, int par, Map<Integer, Set<Integer>> map) {
        if (curr == null) return;
        if (!map.containsKey(curr.val)) {
            map.put(curr.val, new HashSet<>()); // map = {1: []}
        }
        // Get adjacency list of current node
        Set<Integer> adj = map.get(curr.val);
        // Add the parent to the current node's adjacency list (undirected graph edge)
        if (par != 0) {
            adj.add(par);
        }
        if (curr.left != null) {
            adj.add(curr.left.val);
        }
        if (curr.right != null) {
            adj.add(curr.right.val);
        }
        // Recursively convert the left and right subtrees
        convert(curr.left, curr.val, map);
        convert(curr.right, curr.val, map);
    }
}
```

### Time Complexity:
- The time complexity is `O(n)`, where `n` is the number of nodes in the tree. The graph conversion and BFS traversal each take linear time with respect to the number of nodes.

### Space Complexity:
- The space complexity is `O(n)` for storing the graph representation and the queue during BFS. `n` is the number of nodes in the tree.

### Accepted Solution
![image](https://github.com/user-attachments/assets/ff7510b2-c4e7-4b60-82e8-61579305082f)
