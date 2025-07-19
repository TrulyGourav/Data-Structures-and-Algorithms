
# 📘 Longest Increasing Subsequence (LIS)

---

## 📌 Problem Statement

Given an array of integers `nums`, return the **length of the longest strictly increasing subsequence**.

### Example:

```
Input:  nums = [10, 9, 2, 5, 3, 7, 101, 18]  
Output: 4  
Explanation: The LIS is [2, 3, 7, 101].
```

---

## 💡 Intuition (⭐ Highlight)

This is a classic **dynamic programming** problem.

> For each index `i`, we find all `j < i` such that `nums[i] > nums[j]`.  
> Among those, we take the max `dp[j] + 1`.  
> If none found, the LIS ending at `i` is just 1 (the number itself).

You’re building increasing sequences **ending at each index**, and taking the maximum of all.

---

## 🧠 Conceptual Understanding

- Every element can either:
  - Extend an increasing subsequence from before, OR
  - Start a new one.
- We maintain a `dp[]` array where:
  - `dp[i] = length of the LIS ending at index i`.

---

## 🧭 Approach

1. Initialize `dp[i] = 1` for all `i`.
2. For each `i`, check all previous `j < i`.
3. If `nums[i] > nums[j]`, then:
   ```java
   dp[i] = max(dp[i], dp[j] + 1)
   ```
4. Return the maximum value in the `dp[]` array.

---

## 🧪 DP Table (Final `dp[]` Values Only)

For input: `nums = [10, 9, 2, 5, 3, 7, 101, 18]`

```
Index:      0   1   2   3   4   5   6    7
Value:     10   9   2   5   3   7  101  18
DP:         1   1   1   2   2   3   4    4
```

✅ Final LIS Length = `max(dp) = 4`

---

## 💻 Code Solution (Java)

```java
public class Solution {
    public static int lengthOfLIS(int[] nums) {
        int n = nums.length;
        int[] dp = new int[n];
        int maxLen = 1;

        for (int i = 0; i < n; i++) dp[i] = 1;

        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
            maxLen = Math.max(maxLen, dp[i]);
        }

        return maxLen;
    }
}
```

---

## 📊 Time & Space Complexity

| Metric          | Value     |
|------------------|-----------|
| Time Complexity  | O(n²)     |
| Space Complexity | O(n)      |

---

## 🚀 Other Possible Solutions

| Approach                                  | Time      | Space     | Status    |
|------------------------------------------|-----------|-----------|-----------|
| Brute Force (Generate all subsequences)  | O(2ⁿ)     | O(n)      | ❌        |
| **DP - Current Solution**                | ✅ O(n²)  | ✅ O(n)    | ✅ Used   |
| Binary Search + Greedy (Patience Sort)   | O(n log n)| O(n)      | ✅ Optimal |

---

## 🧠 Pattern Recognition

- **Subsequence Problems**
- **DP on Arrays**
- **Classic LIS pattern**

Related problems:
- Longest Bitonic Subsequence
- Number of LIS
- Russian Doll Envelopes
- Longest String Chain

---

## 🧩 Tip to Remember Forever

### 🧱 *“Building a Tower of Increasing Numbers”*

Imagine each number is a **brick**.  
You’re placing bricks one by one, but you can only place a brick **on top of a smaller one**.  
So for each brick:
- Look at all previous smaller bricks.
- Pick the **tallest tower** and place your brick on it.

That’s how the DP array grows:  
`dp[i] = max(dp[j] + 1)` where `nums[i] > nums[j]`

📌 **Visualize it as stacking sorted bricks, one higher than the other.**  
This will stick.
