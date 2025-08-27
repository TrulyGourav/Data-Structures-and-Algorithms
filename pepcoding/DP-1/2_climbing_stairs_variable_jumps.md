# 🧗‍♂️ Climbing Stairs with Variable Jumps (DP)

## 📌 Problem Statement
You are standing at the **0th stair** and want to reach the **nth stair** (top).  
You are given an array `jumps[]` of size `n` where `jumps[i]` represents the **maximum number of steps** you can jump from stair `i`.  

Return the **minimum number of jumps** required to reach the top. If not possible, return `-1`.

### Example 1
Input:  
```
jumps = [3, 3, 0, 2, 2, 3]
```
Explanation:  
- From stair `0`, we can jump up to 3 steps (to 1, 2, or 3).  
- One optimal way: `0 -> 3 -> 5 -> end` (3 jumps).  
Output:  
```
3
```

### Example 2
Input:  
```
jumps = [1, 0, 2, 3]
```
Explanation:  
- From stair `0`, you can only move 1 step to stair `1`.  
- But `jumps[1] = 0`, so you get stuck.  
Output:  
```
-1
```

---

## 💡 Intuition
Imagine you are climbing stairs but each stair has a **springboard** that lets you jump forward by up to `jumps[i]` steps.  
- You always want to minimize the number of springboard uses (jumps).  
- At each stair, you explore **all possible jumps** and recursively decide the minimum jumps needed from there.  
- This naturally screams **Dynamic Programming** because of **overlapping subproblems**:  
  - Many paths will revisit the same stair.

---

## 🌀 Top-Down (Recursive DP with Memoization)

### Approach (Step-by-step thinking like in interview):
1. Define the subproblem:  
   `minJumps(i)` = minimum jumps needed to reach the end from stair `i`.  
2. Base cases:  
   - If `i == n` (end): `0` (we're already at the top).  
   - If `jumps[i] == 0`: we’re stuck → return `∞` (or some large number).  
3. Transition:  
   - From stair `i`, try all jumps `1...jumps[i]`.  
   - Choose the minimum among them.  
4. Memoize results to avoid recomputation.  

### Recursive Code (Java)
```java
int minJumps(int[] jumps, int idx, int[] dp) {
    int n = jumps.length;
    
    // base case: reached the end
    if (idx == n) return 0;
    
    // out of bounds or stuck
    if (idx > n || jumps[idx] == 0) return Integer.MAX_VALUE;
    
    // memoization
    if (dp[idx] != -1) return dp[idx];
    
    int ans = Integer.MAX_VALUE;
    for (int step = 1; step <= jumps[idx]; step++) {
        int next = minJumps(jumps, idx + step, dp);
        if (next != Integer.MAX_VALUE) {
            ans = Math.min(ans, 1 + next);
        }
    }
    
    return dp[idx] = ans;
}
```

### Complexity
- **Time:** `O(n * maxJump)` in worst case (each stair exploring all its possible jumps).  
- **Space:** `O(n)` (recursion stack + memo).  

---

## 📋 Bottom-Up (Tabulation)

### Approach:
1. Create a DP array `dp[]` where `dp[i]` = minimum jumps needed to reach the end from stair `i`.  
2. Initialize:  
   - `dp[n] = 0` (no jumps needed from the end).  
   - Rest = `∞`.  
3. Fill table **backwards** (from `n-1` down to `0`).  
   - From each stair `i`, check all `1...jumps[i]` steps and take minimum.  
4. Answer will be at `dp[0]`.  

### Dry Run (Tabulation Filling)
For `jumps = [3, 3, 0, 2, 2, 3]` and `n = 6`:

- `dp[6] = 0` (at the top).  
- `dp[5] = 1` (one jump to reach end).  
- `dp[4] = 1 + dp[6] = 1` (direct jump to end).  
- `dp[3] = min(1 + dp[4], 1 + dp[5]) = min(2, 2) = 2`.  
- `dp[2] = ∞` (stuck, because `jumps[2] = 0`).  
- `dp[1] = min(1 + dp[2], 1 + dp[3], 1 + dp[4]) = min(∞, 3, 2) = 2`.  
- `dp[0] = min(1 + dp[1], 1 + dp[2], 1 + dp[3]) = min(3, ∞, 3) = 3`.  

So final `dp = [3, 2, ∞, 2, 1, 1, 0]`.

### Bottom-Up Code (Java)
```java
int minJumpsBU(int[] jumps) {
    int n = jumps.length;
    int[] dp = new int[n + 1];
    Arrays.fill(dp, Integer.MAX_VALUE);
    
    dp[n] = 0; // base case
    
    for (int i = n - 1; i >= 0; i--) {
        if (jumps[i] > 0) {
            int min = Integer.MAX_VALUE;
            for (int step = 1; step <= jumps[i] && i + step <= n; step++) {
                if (dp[i + step] != Integer.MAX_VALUE) {
                    min = Math.min(min, dp[i + step]);
                }
            }
            if (min != Integer.MAX_VALUE) {
                dp[i] = 1 + min;
            }
        }
    }
    
    return dp[0] == Integer.MAX_VALUE ? -1 : dp[0];
}
```

### Complexity
- **Time:** `O(n * maxJump)`  
- **Space:** `O(n)`  

---

## 🔗 Related Problems
- Jump Game I (Can you reach the end?).  
- Jump Game II (Minimum jumps to reach end).  
- Minimum Path Sum in Grid.  
- Frog Jump (LeetCode Hard).  

---

## 🧠 Memory Strategy
Think of each stair as a **video game trampoline** 🎮.  
- Some trampolines are powerful (let you jump far).  
- Some are broken (`0`, you get stuck).  
- Your goal is to **minimize trampoline uses** to finish the level.  
Every time you see a "jumping" problem in DP, remember **Mario jumping platforms** 🌉.

---
