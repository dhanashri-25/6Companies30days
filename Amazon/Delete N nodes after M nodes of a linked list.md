# Delete N Nodes After M Nodes of a Linked List

## Problem Description

Given a linked list, delete `n` nodes after skipping `m` nodes of the linked list until the end of the list.

#### Example 1:
**Input:**
```java
Linked List: 9->1->3->5->9->4->10->1, n = 1, m = 2
```

**Output:**
```java
9->1->5->9->10->1
```

**Explanation:**
- Skip 2 nodes (`9->1`) and delete 1 node (`3`).
- Continue skipping 2 nodes (`5->9`) and delete 1 node (`4`).
- The result is `9->1->5->9->10->1`.

## Expected Time Complexity
- `O(n)` where `n` is the number of nodes in the linked list.

## Expected Space Complexity
- `O(1)` since no additional space is used apart from a few pointers.

---

## Solution:

```java
class Solution {
    static void linkdelete(Node head, int n, int m) {
        if (head == null) return;

        Node temp = head;

        while (temp != null) {
            // Skip m nodes
            for (int i = 1; i < m && temp != null; i++) {
                temp = temp.next;
            }

            // After reaching the m-th node, prepare to delete n nodes
            if (temp == null || temp.next == null) return;

            Node curr = temp.next;
            for (int i = 0; i < n && curr != null; i++) {
                Node prev = temp;
                prev.next = curr.next; // Skip the current node
                curr = curr.next; // Move to the next node
            }

            // Move temp to the next position after deletion
            temp = curr;
        }
    }
}
```

---

### Time Complexity:
- **Skipping `m` nodes:** Takes `O(n)` in total across all iterations.
- **Deleting `n` nodes:** Takes `O(n)` in total across all iterations.
- Overall: **`O(n)`**.

### Space Complexity:
- **Space used:** `O(1)` since no additional data structures are used.

---
