# 🪜 Climbing Stairs (DP Notes)

## 📌 Problem Statement
You are climbing a staircase. It takes `n` steps to reach the top.  
Each time you can either climb **1 step** or **2 steps**.  

Return the total number of **distinct ways** you can climb to the top.

### Example 1:
```
Input: n = 2
Output: 2
Explanation: Two ways to climb:
  1. 1 step + 1 step
  2. 2 steps
```

### Example 2:
```
Input: n = 3
Output: 3
Explanation: Three ways to climb:
  1. 1 + 1 + 1
  2. 1 + 2
  3. 2 + 1
```

---

## 💡 Intuition
This problem is very similar to the **Fibonacci sequence**.

- To reach the `n`th stair, the **last move** could have been:
  - from `(n-1)`th stair (1 step jump), OR  
  - from `(n-2)`th stair (2 step jump).  

👉 So, `ways(n) = ways(n-1) + ways(n-2)`.

We just need to find this recurrence in both recursive (top-down) and iterative (bottom-up) styles.

---

## 🧩 Approach 1: Top-Down (Recursive + Memoization)

### Step-by-step Thinking:
1. Start at step `n`.  
2. Think backwards: "To reach `n`, I must have come from `n-1` or `n-2`".  
3. This gives a recursive formula: `f(n) = f(n-1) + f(n-2)`.  
4. Add base cases:  
   - `f(0) = 1` (1 way to stay at ground).  
   - `f(1) = 1` (only one way: 1 step).  
5. Use **memoization** to avoid recomputing the same states.

---

### ⌨️ Code (Top-Down in Java)
```java
int climbStairs(int n) {
    int[] dp = new int[n + 1];
    Arrays.fill(dp, -1);
    return solve(n, dp);
}

private int solve(int n, int[] dp) {
    if (n == 0 || n == 1) return 1;  // base cases
    if (dp[n] != -1) return dp[n];   // already computed
    return dp[n] = solve(n - 1, dp) + solve(n - 2, dp);
}
```

---

### ⏱️ Complexity (Top-Down)
- **Time:** `O(n)` (each state solved once).  
- **Space:** `O(n)` (stack space + memo array).  

---

## 🧩 Approach 2: Bottom-Up (Tabulation)

### Step-by-step Thinking:
Instead of recursion, we fill a **DP table** from the ground up.

1. Create `dp[]` of size `n+1`.  
2. Base cases:  
   - `dp[0] = 1`  
   - `dp[1] = 1`  
3. For each `i` from `2` to `n`:  
   - `dp[i] = dp[i-1] + dp[i-2]`.  

This fills the table like Fibonacci.

---

### 🏗️ How the Table Fills (Example: n=5)
```
dp[0] = 1
dp[1] = 1

Now fill:
dp[2] = dp[1] + dp[0] = 1 + 1 = 2
dp[3] = dp[2] + dp[1] = 2 + 1 = 3
dp[4] = dp[3] + dp[2] = 3 + 2 = 5
dp[5] = dp[4] + dp[3] = 5 + 3 = 8

Final Answer = dp[5] = 8
```

---

### ⌨️ Code (Bottom-Up in Java)
```java
int climbStairs(int n) {
    if (n == 0 || n == 1) return 1;
    int[] dp = new int[n + 1];
    dp[0] = dp[1] = 1;

    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    return dp[n];
}
```

---

### ⏱️ Complexity (Bottom-Up)
- **Time:** `O(n)` (loop from 2..n).  
- **Space:** `O(n)` (array of size n).  
- Can be **optimized to O(1)** space by keeping only last two values.

---

## 🔗 Related Problems
- **Fibonacci Number** (exact same logic).  
- Min Cost Climbing Stairs (variation with weights).  
- Ways to Decode (similar recurrence with constraints).  
- Unique Paths (grid version).  

---

## 🎯 Strategy to Remember
Imagine you’re **climbing stairs with two legs**:
- One leg always goes **1 step**.  
- Other leg can sometimes **jump 2 steps**.  
To reach the top, you must decide which leg’s move got you there.  
This **two-leg thinking = f(n-1) + f(n-2)**.  

Or fun analogy:  
Think of Netflix binge-watching.  
- You can watch **1 episode** at a time or **skip ahead by 2**.  
- The number of ways to finish a season of `n` episodes = Climbing Stairs DP 😆.
