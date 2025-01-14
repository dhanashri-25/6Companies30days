# Excel Sheet Column Title
[Problem Link](https://leetcode.com/problems/excel-sheet-column-title/)

## Problem Description
Given an integer `columnNumber`, return its corresponding column title as it appears in an Excel sheet.

### Mapping:
- `A -> 1`
- `B -> 2`
- `C -> 3`
- ...
- `Z -> 26`
- `AA -> 27`
- `AB -> 28`
- ...
  
### Examples

#### Example 1:
**Input:**  
`columnNumber = 1`  
**Output:**  
`"A"`

---

#### Example 2:
**Input:**  
`columnNumber = 28`  
**Output:**  
`"AB"`

---

#### Example 3:
**Input:**  
`columnNumber = 701`  
**Output:**  
`"ZY"`

---

### Code:
```java
class Solution {
    public String convertToTitle(int columnNumber) {
        StringBuilder result = new StringBuilder();
        
        while (columnNumber > 0) {
            columnNumber--; // Adjust to 0-based indexing
            int remainder = columnNumber % 26;
            result.insert(0, (char) ('A' + remainder)); // Prepend the character
            columnNumber /= 26; // Move to the next significant position
        }
        
        return result.toString();
    }
}
```

---

## Explanation with Example:
### Input:
`columnNumber = 28`

### Iterations:
1. **Initial State:**  
   `columnNumber = 28`

2. **First Iteration:**  
   - `columnNumber-- = 27`
   - `remainder = 27 % 26 = 1`
   - Append `'A' + 1 = 'B'`
   - Update: `columnNumber = 27 / 26 = 1`

3. **Second Iteration:**  
   - `columnNumber-- = 0`
   - `remainder = 0 % 26 = 0`
   - Append `'A' + 0 = 'A'`
   - Update: `columnNumber = 0`

### Final Result:
`"AB"`

---

## Complexity Analysis
1. **Time Complexity:**  
   - Each iteration reduces `columnNumber` by a factor of 26.
   - Number of iterations ≈ `O(log26(columnNumber))`
   - Overall: **`O(log(columnNumber))`**

2. **Space Complexity:**  
   - Using a `StringBuilder` for the result.
   - Overall: **`O(log(columnNumber))`**

---
## Accepted Solution
![image](https://github.com/user-attachments/assets/f88adab0-0524-4016-8554-7fa63eaa4729)
