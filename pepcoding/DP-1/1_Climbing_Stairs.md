# DP Notes: Climbing Stairs (Number of Ways)

## 1) Refined Problem Statement
You are on **stair 0** and want to reach **stair n**. At each move, you may climb **1 step** or **2 steps**.  
**Return the number of distinct ways** to reach stair `n`.

- You start at step `0`. Reaching step `n` exactly counts as one complete way.
- It’s allowed to take different sequences of 1s and 2s (order matters).
- Assume `0 ≤ n ≤ 10^5` (typical interview constraints allow linear DP).

**Edge cases**
- `n = 0` → **1** way (do nothing).
- `n = 1` → **1** way: `[1]`.
- `n = 2` → **2** ways: `[1,1]`, `[2]`.

**Examples**
- `n = 3` → ways: `[1,1,1]`, `[1,2]`, `[2,1]` → **3**
- `n = 4` → `[1,1,1,1]`, `[1,1,2]`, `[1,2,1]`, `[2,1,1]`, `[2,2]` → **5**

> This is the **Fibonacci-like** recurrence: `ways(n) = ways(n-1) + ways(n-2)` with base `ways(0)=1`, `ways(1)=1`.

---

## 2) Intuition & Step-by-Step Human Thinking

**How do I think about it?**  
Standing at step `n`, the *last jump* had to be either:
- from `n-1` using a `+1` step, or
- from `n-2` using a `+2` step.

So **every** valid path to `n` ends with one of those two choices. These two sets of paths are **disjoint** and **cover all** possibilities, so:
```
ways(n) = ways(n-1) + ways(n-2)
```
Start the recurrence by asking: “What are the trivial counts?”  
- To reach step `0`: exactly **1** way (do nothing).  
- To reach step `1`: exactly **1** way (`[1]`).

From here, everything builds up.

### When to choose Top-Down vs Bottom-Up?
- **Top-Down (Recursive + Memo)** mirrors the natural recurrence; great for clarity.  
- **Bottom-Up (Tabulation)** iteratively fills answers and can be easily **space-optimized** to O(1), which is production-friendly.

---

## 3) Top-Down (Recursive + Memoization)

### Intuition & Approach
1. Define `f(n)` = number of ways to reach stair `n`.
2. Base cases: `f(0)=1`, `f(1)=1`.
3. Recurrence: `f(n)=f(n-1)+f(n-2)`.
4. Use a memo map/array to avoid recomputing `f(k)` for the same `k`.
5. Answer is `f(n)`.

### Java — Expected Method Only
```java
// Top-Down: O(n) time, O(n) space (memo + recursion stack)
public int climbStairs(int n) {
    int[] memo = new int[n + 1];
    Arrays.fill(memo, -1);
    return dfs(n, memo);
}

private int dfs(int n, int[] memo) {
    if (n == 0 || n == 1) return 1;
    if (memo[n] != -1) return memo[n];
    memo[n] = dfs(n - 1, memo) + dfs(n - 2, memo);
    return memo[n];
}
```

**Notes**
- `memo[n]` stores `f(n)` once computed.
- Recursion depth is `O(n)`; safe for typical `n` in interviews.

---

## 4) Bottom-Up (Tabulation)

### Intuition & Approach
We **build from the base** upward, filling a DP table where `dp[i]` = number of ways to reach stair `i`.
- Initialize `dp[0]=1`, `dp[1]=1`.
- For `i` from `2` to `n`: `dp[i]=dp[i-1]+dp[i-2]`.

### How the table fills (example `n=5`)
Start with:
```
i   : 0  1  2  3  4  5
dp  : 1  1  -  -  -  -
```
Fill step by step:
- `dp[2] = dp[1] + dp[0] = 1 + 1 = 2`
- `dp[3] = dp[2] + dp[1] = 2 + 1 = 3`
- `dp[4] = dp[3] + dp[2] = 3 + 2 = 5`
- `dp[5] = dp[4] + dp[3] = 5 + 3 = 8`

Final table:
```
i   : 0  1  2  3  4  5
dp  : 1  1  2  3  5  8
```
Answer: `dp[5] = 8`.

### Java — Expected Method Only (Tabulation)
```java
// Bottom-Up: O(n) time, O(n) space
public int climbStairs(int n) {
    if (n <= 1) return 1;
    int[] dp = new int[n + 1];
    dp[0] = 1;
    dp[1] = 1;
    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
}
```

### Space-Optimized Tabulation (Optional best practice)
We only need the previous two values:
```java
// Bottom-Up Space-Optimized: O(n) time, O(1) space
public int climbStairs(int n) {
    if (n <= 1) return 1;
    int prev2 = 1; // f(0)
    int prev1 = 1; // f(1)
    for (int i = 2; i <= n; i++) {
        int cur = prev1 + prev2;
        prev2 = prev1;
        prev1 = cur;
    }
    return prev1; // f(n)
}
```

---

## 5) Time & Space Complexity

| Approach | Time | Space |
|---|---|---|
| Top-Down (Memo) | `O(n)` | `O(n)` for memo + recursion stack |
| Bottom-Up (Tabulation) | `O(n)` | `O(n)` |
| Bottom-Up (Space-Optimized) | `O(n)` | `O(1)` |

---

## 6) Relevant Problems (Same Pattern / Intuition)
- **Fibonacci Number** (classic identical recurrence / bases).  
- **Min Cost Climbing Stairs** (same state movement + cost aggregation).  
- **Ways to Decode (LeetCode 91)** (branching by 1- or 2-digit choices).  
- **House Robber** (choose current vs previous best → depends on `i-1`, `i-2`).  
- **Tiling a 2×n board with 2×1 dominoes** (tiling recurrence).  
- **Frog Jump (basic variant with 1 or 2 jumps)**.  
- **Count ways to reach n with steps in {1,2,k}** (straight generalization).

---

## 7) Strategy to Remember (Sticky Analogy)
**“Two Doors to the Penthouse”** 🏢  
Imagine each floor `i` has exactly **two doors** that can lead **into** it:  
- Door A from floor `i-1` (1-step),  
- Door B from floor `i-2` (2-step).  
To count all visitor routes to floor `i`, **add** the number of routes that reached `i-1` and `i-2`. Repeat floor by floor from the lobby (0) upward.  
That’s why the count **adds** like Fibonacci. If you can picture doors feeding into each floor, your brain will auto-remember: `dp[i] = dp[i-1] + dp[i-2]` with `dp[0]=1`, `dp[1]=1`.

---

## 8) Quick Recap
- Model states as “ways to reach this step.”
- Base truths: `ways(0)=1`, `ways(1)=1`.
- Transition: from `i-1` or `i-2` → **add** the counts.
- Tabulate left-to-right or memoize top-down.  
- Space-optimize using two rolling variables.

---

## 9) Common Pitfalls
- Returning `0` for `n=0` (should be `1` – doing nothing is one valid way).  
- Off-by-one errors when allocating arrays (`n+1` size).  
- Mixing **min/max** DP with **counting** DP (remember: this problem is pure counting, not optimization).

---

*Happy climbing!* 🧗‍♂️
