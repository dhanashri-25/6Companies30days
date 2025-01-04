### Problem: Bulls and Cows
[Problem Link](https://leetcode.com/problems/bulls-and-cows/description/)

You are playing a game with your friend where you write down a secret number, and your friend guesses the number. Based on the guess, you return a hint:

- **Bulls (x)**: The number of digits that are in the correct position.
- **Cows (y)**: The number of digits that are in the secret number but in the wrong position (i.e., the non-bull digits that can be rearranged to form bulls).

The hint should be returned in the format `"xAyB"`, where `x` is the number of bulls and `y` is the number of cows.

### Example 1:

**Input:**
```java
secret = "1807", guess = "7810"
```

**Output:**
```java
"1A3B"
```

**Explanation:**
- Bulls: `1` is in the correct position (position 1 in both strings).
- Cows: `7`, `8`, and `0` are all correct digits but in the wrong positions.

### Example 2:

**Input:**
```
secret = "1123", guess = "0111"
```

**Output:**
```
"1A1B"
```

**Explanation:**
- Bulls: `1` at position 1 is in the correct position.
- Cows: Only one `1` can be counted as a cow because the unmatched `1`s can only be rearranged once.

---

### Solution Explanation

#### Steps:
1. Traverse both strings (`secret` and `guess`) and check if the digits match in the same position. If they do, it's a bull.
2. If a digit does not match, track its occurrence in both strings using a frequency array.
3. The frequency array helps track unmatched digits and allows us to count cows correctly.
   - When a digit from the guess is present in the secret and has been unmatched before, it can be counted as a cow.
4. Finally, return the result in the format `"xAyB"`.

---

### Code

```java
class Solution {
    public String getHint(String secret, String guess) {
        int bulls = 0;  // Correct position and value
        int cows = 0;   // Correct value but wrong position
        int[] numbers = new int[10];  // Track the frequency of digits (0-9)

        for (int i = 0; i < secret.length(); i++) {
            // Numeric values of characters
            int s = secret.charAt(i) - '0';  // Convert char to int
            int g = guess.charAt(i) - '0';   // Convert char to int

            // If the digits at the same index in both strings match, it's a bull
            if (s == g) {
                bulls++;  // Increment the bull counter
            } else {
                // If s is not matched yet, increment its frequency (it may be a cow later)
                if (numbers[s] < 0)
                    cows++;  // This means there are unmatched occurrences of 's' from previous iterations
                // If g has appeared in the secret before, increment cows
                if (numbers[g] > 0)
                    cows++;  // This means there are unmatched occurrences of 'g' from previous iterations

                // Update the frequency of the digits in the 'numbers' array
                numbers[s]++;  // Increment the count of 's' (digit from 'secret')
                numbers[g]--;  // Decrement the count of 'g' (digit from 'guess')
            }
        }

        // Return the result in the format "xAyB"
        return bulls + "A" + cows + "B";
    }
}
```

---

### Time Complexity:

- **O(n)**, where `n` is the length of the input strings (`secret` and `guess`). We loop through each digit of the strings once and perform constant time operations within the loop.

---

### Explanation in Simple Terms:

1. **Bulls** are the digits that are exactly the same at the same position in both the `secret` and `guess` strings. We count these first.
2. **Cows** are the digits that exist in the secret number but are at the wrong position in the guess. We track the unmatched digits from both strings using the `numbers` array and adjust the count of cows accordingly.
3. The result is returned in the format `"xAyB"`, where `x` is the count of bulls and `y` is the count of cows.