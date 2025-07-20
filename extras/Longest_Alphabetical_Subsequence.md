# 📘 Longest Alphabetical Subsequence

## 📌 Problem Statement
Given a string `s`, find the **length of the longest subsequence** (not necessarily contiguous) such that the characters of the subsequence are in **strictly increasing alphabetical order**.

---

## 💡 Intuition (⭐)
We are looking for the **longest increasing subsequence (LIS)** — but instead of **integers**, we're working with **characters (alphabets)**.

### Key Insight:
> If `s.charAt(j) < s.charAt(i)`, and we already know the longest increasing subsequence ending at `j`, we can extend that by including `s.charAt(i)`.

This is **exactly like the LIS problem on an array of integers**, but instead, we compare characters.

---

## 🧠 Conceptual Understanding
- Every character can start a new increasing subsequence.
- We try to **extend existing subsequences** by finding previous characters that are smaller.
- So, we **build a dp array** where `dp[i]` = length of the longest increasing subsequence ending at index `i`.

---

## 🧭 Approach
1. Initialize `dp[i] = 1` for all characters, as every single character is a valid subsequence.
2. For every character `s[i]`, compare it with previous characters `s[j]` (for `j < i`).
3. If `s[j] < s[i]`, update:  
   `dp[i] = max(dp[i], dp[j] + 1)`
4. Finally, return the max of all `dp[i]` values.

---

## 🧪 Example + DP Table

Let’s consider: `s = "abcbdab"`

| Index (i) | Char | Compare With | Condition Met | dp[i] Update               | dp[i] |
|-----------|------|--------------|----------------|----------------------------|--------|
| 0         | a    | -            | -              | base case                  | 1      |
| 1         | b    | a            | b > a          | dp[1] = max(1, dp[0]+1) = 2| 2      |
| 2         | c    | a, b         | c > a, b       | dp[2] = max(1, dp[1]+1) = 3| 3      |
| 3         | b    | a            | b > a          | dp[3] = max(1, dp[0]+1) = 2| 2      |
| 4         | d    | a,b,c,b      | d > all        | dp[4] = max(1, dp[2]+1) = 4| 4      |
| 5         | a    | -            | no increase    | dp[5] = 1                  | 1      |
| 6         | b    | a            | b > a          | dp[6] = max(1, dp[5]+1)=2  | 2      |

🟩 Final `dp = [1, 2, 3, 2, 4, 1, 2]`  
✅ **Answer = max(dp) = 4**, the length of `"abcd"`

---

## 💻 Code Solution (Java)

```java
public class Solution {

    public static int longestSubseq(String s) {
        int n = s.length();
        int[] dp = new int[n];
        int maxLen = 1;

        // Initialize all to 1 (each character is a valid subsequence)
        for (int i = 0; i < n; i++) dp[i] = 1;

        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (s.charAt(i) > s.charAt(j)) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
            maxLen = Math.max(maxLen, dp[i]);
        }

        return maxLen;
    }

    public static void main(String[] args) {
        String s = "abcbdab";
        System.out.println("Longest Alphabetical Subsequence: " + longestSubseq(s));
    }
}
```

---

## 📊 Time & Space Complexity

| Aspect       | Complexity |
|--------------|------------|
| Time         | O(n²)      |
| Space        | O(n)       |

---

## 🚀 Other Possible Solutions

| Approach                                  | Time      | Space     | Notes                        |
|------------------------------------------|-----------|-----------|------------------------------|
| Brute-force (generate all subsequences)  | O(2ⁿ)     | O(n)      | Inefficient for large input |
| Greedy (incorrect)                       | -         | -         | Fails, doesn’t consider all |
| ✅ DP (your current solution)            | O(n²)     | O(n)      | Standard DP-based LIS logic |
| Patience Sorting + Binary Search (LIS)   | O(n log k)| O(n)      | Can be adapted using TreeMap/array |

---

## 🧠 Pattern Recognition

- **LIS Variant**
- **Subsequence + Increasing Pattern**

### Similar Problems
- [LIS - Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)
- Longest Bitonic Subsequence
- Number of LIS
- Longest Chain of Pairs

---

## 🧩 Tip to Remember Forever

### 🎯 Think of building a tower of letters!

Imagine placing each letter like a block.
You **can only stack a letter** on top of a smaller one alphabetically.

For each new block, look at all smaller blocks before it — what’s the tallest tower you can build up to this point?

> 🧠 Mentally map it to **"Longest Tower Building" using alphabetical bricks**

Once you visualize letters like Lego blocks going upward → it becomes intuitive.

---
