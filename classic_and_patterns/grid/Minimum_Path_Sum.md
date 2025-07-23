
# 🚀 64. Minimum Path Sum

**Difficulty**: Medium  
**Platform**: LeetCode  
**Link**: [https://leetcode.com/problems/minimum-path-sum/](https://leetcode.com/problems/minimum-path-sum/)  

---

## 🧩 Problem Statement

You are given an `m x n` grid filled with non-negative numbers.  
Find a path from the **top-left** to the **bottom-right**, which **minimizes the sum** of all numbers along its path.

🔹 You can only move **right or down** at any point.

---

## 💡 Intuition

Think like a human first: If you want to go from top-left to bottom-right in a grid, and can only go right or down, at each step you want to pick the **minimum cost** path moving forward.

So, for each cell, you want to know:  
**“What is the minimum cost to reach this cell?”**  
From where can you reach it? Only from:
- The **top** (if not on first row)
- The **left** (if not on first column)

Therefore:  
👉 Minimum cost to reach `(i,j)` is:  
`grid[i][j] += min(grid[i-1][j], grid[i][j-1])`  

Start from top-left (0,0) and move forward filling each cell with the **minimum path sum** required to reach it.

---

## 🔁 Approaches

### 1️⃣ Recursion (Brute-force)

#### 🔍 Idea:
Try all paths going right and down recursively.

```java
int solve(int i, int j, int[][] grid) {
    if (i == 0 && j == 0) return grid[0][0];
    if (i < 0 || j < 0) return Integer.MAX_VALUE;
    int up = solve(i - 1, j, grid);
    int left = solve(i, j - 1, grid);
    return grid[i][j] + Math.min(up, left);
}
```

#### ⏱ Time Complexity:
Exponential — `O(2^(m*n))`

#### 🧠 Intuition:
Explore all possible paths.

---

### 2️⃣ Recursion + Memoization

#### 🔍 Idea:
Memoize the result of `(i,j)` using a `dp[i][j]` array.

```java
int solve(int i, int j, int[][] grid, int[][] dp) {
    if (i == 0 && j == 0) return grid[0][0];
    if (i < 0 || j < 0) return Integer.MAX_VALUE;
    if (dp[i][j] != -1) return dp[i][j];
    int up = solve(i - 1, j, grid, dp);
    int left = solve(i, j - 1, grid, dp);
    return dp[i][j] = grid[i][j] + Math.min(up, left);
}
```

#### ⏱ Time: `O(m*n)` | 🧠 Space: `O(m*n)` (stack + memo table)

---

### 3️⃣ Tabulation (Bottom-Up DP) ✅ Optimal

```java
public int minPathSum(int[][] grid) {
    int m = grid.length;
    int n = grid[0].length;
    
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (i == 0 && j == 0) continue; // start point
            else if (i == 0) grid[i][j] += grid[i][j - 1];
            else if (j == 0) grid[i][j] += grid[i - 1][j];
            else grid[i][j] += Math.min(grid[i - 1][j], grid[i][j - 1]);
        }
    }
    return grid[m - 1][n - 1];
}
```

#### ✅ We reuse the `grid` itself as the `dp` table!

---

## 📊 Sample Execution Trace (Tabulation)

### Input:

```
[ [1, 3, 1],
  [1, 5, 1],
  [4, 2, 1] ]
```

### After filling DP Table:

```
[ [1, 4, 5],
  [2, 7, 6],
  [6, 8, 7] ]
```

### Result is in bottom-right cell: `7`

---

## 🧮 DP Cell Explanation (Example: dp[1][2])

`dp[1][2]` = minimum sum to reach cell `(1,2)`

Can come from:
- Top: `dp[0][2]` = 5
- Left: `dp[1][1]` = 7

So:  
`dp[1][2] = grid[1][2] + min(5, 7)`  
`= 1 + 5 = 6` ✅

---

## 📚 All Approaches Summary

| Approach             | Time Complexity | Space Complexity | Note                  |
|----------------------|------------------|-------------------|------------------------|
| Brute-force Recursion | Exponential      | Exponential        | ❌ Inefficient          |
| Rec + Memoization     | O(m*n)           | O(m*n)             | ✅ Better               |
| Tabulation (DP)       | O(m*n)           | O(1)               | ✅✅ Best (in-place grid update) |

---

## 🔗 Related Problems

| Problem Name | Description | Link |
|--------------|-------------|------|
| Unique Paths | Count number of ways to reach bottom-right | [62. Unique Paths](https://leetcode.com/problems/unique-paths/) |
| Unique Paths II | Same as Unique Paths but with obstacles | [63. Unique Paths II](https://leetcode.com/problems/unique-paths-ii/) |
| Triangle | Minimum path sum in a triangle (bottom-up DP) | [120. Triangle](https://leetcode.com/problems/triangle/) |
| Minimum Falling Path Sum | Allows downward diagonal movement | [931. Minimum Falling Path Sum](https://leetcode.com/problems/minimum-falling-path-sum/) |
| Minimum Path Sum | Min cost path from top-left to bottom-right | [64. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/) |
| Dungeon Game | Min health needed to save princess | [174. Dungeon Game](https://leetcode.com/problems/dungeon-game/) |
| Out of Boundary Paths | Count paths that exit the grid | [576. Out of Boundary Paths](https://leetcode.com/problems/out-of-boundary-paths/) |
| Number of Paths with Max Score | Combine score + path counting | [1301. Number of Paths with Maximum Score](https://leetcode.com/problems/number-of-paths-with-maximum-score/) |
| Number of Ways to Arrive at Destination | Dijkstra variation with path count | [1976. Number of Ways to Arrive at Destination](https://leetcode.com/problems/number-of-ways-to-arrive-at-destination/) |
| Number of Ways to Stay in the Same Place | DP with constrained moves | [1269. Number of Ways to Stay in the Same Place](https://leetcode.com/problems/number-of-ways-to-stay-in-the-same-place-after-some-steps/) |

---

## 📘 GFG Problems to Practice

| Problem Name | Description | Link |
|--------------|-------------|------|
| Minimum Cost Path | Basic variation on cost minimization | [Min Cost Path](https://www.geeksforgeeks.org/min-cost-path-dp-6/) |
| Max Value Path in Matrix | Max path instead of min | [Maximum Path Sum in Matrix](https://www.geeksforgeeks.org/maximum-path-sum-in-matrix/) |
| Number of Paths with Exactly K Coins | Use DP to count specific cost paths | [Number of Paths with Exactly K Coins](https://www.geeksforgeeks.org/number-paths-exactly-k-coins/) |
| Count All Paths Top-Left to Bottom-Right | Pure combinatorics path count | [Count All Paths](https://www.geeksforgeeks.org/count-possible-paths-top-left-bottom-right-nxm-matrix/) |

---

## 🧠 Memory Tip

> "At every step, I bring along the cheapest history."  
Think of it like: You're carrying a backpack of minimum weight from top-left, adding only the lightest between top and left paths.

So:  
`dp[i][j] = cost here + min(top, left)` ➝ Update your journey based on cheapest so far.

---

Happy coding and pattern mastering! 🚀💪
