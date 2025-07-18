# Generate All Subsequences of a String

## 📜 Problem Statement

Given a string `s`, generate and return a list of **all subsequences** (including the empty string).  
A **subsequence** is a sequence that can be derived from the string by deleting **zero or more characters**, without changing the order of the remaining characters.

> Input: `"abc"`  
> Output: `["", "c", "b", "bc", "a", "ac", "ab", "abc"]` (Order may vary)

---

## 💡 Intuition (🌟 Highlighted)

> A subsequence is formed by **either taking or skipping each character** from the string — that's it!

So, at each character, we have **two choices**:
- Include it in the current subsequence.
- Skip it and move to the next.

This naturally forms a **binary decision tree**, and recursion is a perfect way to explore it.

If the string has length `n`, then the total number of subsequences is `2ⁿ`.

---

## 🧠 Conceptual Understanding

### 🔁 Recursion Tree

For `s = "abc"`:
```
                                 ""
                        /                  \
                     "a"                  ""
                  /      \              /     \
               "ab"     "a"         "b"     ""
              /   \     /  \        /  \    /  \
          "abc" "ab" "ac" "a"   "bc" "b" "c"  ""
```

Every level represents a decision:
- Level 0: start
- Level 1: decision for 'a'
- Level 2: decision for 'b'
- Level 3: decision for 'c'

Each path represents one valid subsequence.

---

## 🧭 Approach

### ✅ Recursive DFS (Backtracking Style)

1. Start with empty string and index `0`.
2. For each character:
   - Include it → move to next index
   - Exclude it → move to next index
3. Base case: if index == s.length(), add current string to result.

### 🧮 Generic Formula:

At index `i`:
```
allSubsequences(i, current) = 
    allSubsequences(i+1, current + s[i])   // include
    +
    allSubsequences(i+1, current)          // exclude
```

---

## 📟 Code Solution (Java)
```java
class Solution {
    public List<String> allSubsequences(String s) {
        List<String> result = new ArrayList<>();
        generateSubsequences(s, 0, "", result);
        return result;
    }

    private void generateSubsequences(String s, int index, String current, List<String> result) {
        // Base case: end of string
        if (index == s.length()) {
            result.add(current);  // Add formed subsequence
            return;
        }

        // Choice 1: Include current character
        generateSubsequences(s, index + 1, current + s.charAt(index), result);

        // Choice 2: Exclude current character
        generateSubsequences(s, index + 1, current, result);
    }
}
```

---

## 📊 Time and Space Complexity

| Metric              | Value                |
|---------------------|----------------------|
| Time Complexity     | `O(2^n)`             |
| Space Complexity    | `O(2^n * n)`         |
| Auxiliary Stack     | `O(n)` (call stack)  |

> Since each of the `2^n` subsequences can be up to length `n`, space used for results is `O(2^n * n)`.

---

## 📘 DP Table (Conceptual View)

We can simulate a DP table **like a binary tree of choices**. Each level represents a decision point for a character.

For `s = "abc"`, simulate with table:

| Index | Current Subsequence | Include Char | Exclude Char |
|-------|----------------------|--------------|--------------|
| 0     | ""                   | "a"          | ""           |
| 1     | "a"                  | "ab"         | "a"          |
| 1     | ""                   | "b"          | ""           |
| 2     | "ab"                 | "abc"        | "ab"         |
| 2     | "a"                  | "ac"         | "a"          |
| 2     | "b"                  | "bc"         | "b"          |
| 2     | ""                   | "c"          | ""           |

The final result is:  
`["abc", "ab", "ac", "a", "bc", "b", "c", ""]`

---

## 🚀 Other Possible Solutions & Complexity Comparison

| Approach                              | Time      | Space       | Notes                          |
|---------------------------------------|-----------|-------------|--------------------------------|
| Brute-force via Binary Mask (Bitmask) | `O(2^n)`  | `O(2^n * n)`| Convert each bitmask to string |
| ✅ Recursive Backtracking (Current)   | `O(2^n)`  | `O(2^n * n)`| Elegant, easy to implement     |

---

## 🧠 Pattern Recognition

This problem belongs to the following key patterns:

- ✅ **Recursion + Backtracking**
- ✅ **Binary Decision Tree**
- ✅ **Subset/Power Set Generation**
- ✅ **Bitmasking (Alternative approach)**

---

## 🔗 Similar Problems

| Problem                               | Pattern        |
|---------------------------------------|----------------|
| Subsets I (LeetCode 78)               | Backtracking   |
| Subsets II (With Duplicates)          | Backtracking   |
| Palindromic Subsequences              | DP + Recursion |
| Longest Common Subsequence (LCS)      | DP             |
| Count of Subsequences with Conditions | DP             |

---

## 🧩 Tip to Remember Forever

### 🔑 Trick:
Think of **subsequences like “on/off switches”** for each character.

Each character can be:
- ON (included)
- OFF (excluded)

That’s like flipping a switch: 2 options → binary tree!

🧠 Mnemonic:
> “**Every char has a choice — Include Me or Skip Me**”  
This phrase matches the exact recursive call logic.

👀 Visual:
If you imagine a string like `"abc"`, imagine lights turning on/off:
- `[ON, OFF, ON]` → `"ac"`
- `[OFF, OFF, ON]` → `"c"`

So just think of it like building subsets of characters using switches.