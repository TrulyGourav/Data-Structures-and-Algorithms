# 1536. Minimum Swaps to Arrange a Binary Grid

## 🔗 Problem Link

LeetCode:
https://leetcode.com/problems/minimum-swaps-to-arrange-a-binary-grid/

------------------------------------------------------------------------

# 🧩 Problem Statement

Given an `n x n` binary grid, in one step you can choose two **adjacent
rows** and swap them.

A grid is said to be **valid** if all the cells above the main diagonal
are zeros.

Return the **minimum number of steps** needed to make the grid valid, or
`-1` if it cannot be made valid.

------------------------------------------------------------------------

# 🧠 Core Observation

For row `i`, all cells at positions `j > i` must be `0`.

That means:

Row 0 → needs `n-1` trailing zeros\
Row 1 → needs `n-2` trailing zeros\
Row 2 → needs `n-3` trailing zeros\
... Row i → needs `n-1-i` trailing zeros

💡 So instead of thinking about the full grid, we only care about:

> **How many trailing (suffix) zeros does each row have?**

------------------------------------------------------------------------

# 🌟 INTUITION (Most Important Section)

Instead of rearranging the grid blindly:

1.  Compute trailing zeros for every row.
2.  For position `i`, we need a row having at least `n-1-i` trailing
    zeros.
3.  If such a row exists below, bring it up using adjacent swaps.
4.  If not → impossible.

This is essentially:

> 🔥 Greedy + Bubble-Up Strategy

At every position, choose the first row that satisfies the requirement
and bubble it upward.

We do NOT try all permutations. We fix rows one by one from top to
bottom.

------------------------------------------------------------------------

# 🧮 Example

Input:

    grid =
    [
     [0,0,1],
     [1,1,0],
     [1,0,0]
    ]

Trailing zeros:

    Row 0 → 0
    Row 1 → 1
    Row 2 → 2

Requirements:

    Row 0 needs 2
    Row 1 needs 1
    Row 2 needs 0

We find row with \>=2 → Row 2\
Swap upward → 2 swaps

Then next position works automatically.

Answer = 2

------------------------------------------------------------------------

# 🌳 Visualization of Bubble Process

Suppose suffixZeros = \[0, 1, 2\]

We need 2 at index 0.

           0
           1
           2   ← found here (index 2)

Swap upward:

Step 1: 0 2 1

Step 2: 2 0 1

Swaps = 2

------------------------------------------------------------------------

# 🏗 Conceptual Understanding

This problem reduces to:

1.  Converting matrix condition → trailing zero requirement.
2.  Greedy placement row by row.
3.  Counting minimum adjacent swaps (bubble sort style).

This is similar to:

-   Minimum swaps in restricted bubble sort
-   Greedy row placement problems
-   Stable row reordering

------------------------------------------------------------------------

# ⏱ Time & Space Complexity

### Time Complexity

-   Computing suffix zeros → O(n²)
-   Searching row for each index → O(n²)
-   Total → **O(n²)**

### Space Complexity

-   suffixZeros array → O(n)

------------------------------------------------------------------------

# 💻 Code Solution (Given Approach)

``` java
class Solution {
  public int minSwaps(int[][] grid) {
    final int n = grid.length;
    int ans = 0;
    int[] suffixZeros = new int[n];

    for (int i = 0; i < grid.length; ++i)
      suffixZeros[i] = getSuffixZeroCount(grid[i]);

    for (int i = 0; i < n; ++i) {
      final int neededZeros = n - 1 - i;
      final int j = getFirstRowWithEnoughZeros(suffixZeros, i, neededZeros);
      if (j == -1)
        return -1;

      for (int k = j; k > i; --k)
        suffixZeros[k] = suffixZeros[k - 1];

      ans += j - i;
    }

    return ans;
  }

  private int getSuffixZeroCount(int[] row) {
    for (int i = row.length - 1; i >= 0; --i)
      if (row[i] == 1)
        return row.length - i - 1;
    return row.length;
  }

  private int getFirstRowWithEnoughZeros(int[] suffixZeros, int i, int neededZeros) {
    for (int j = i; j < suffixZeros.length; ++j)
      if (suffixZeros[j] >= neededZeros)
        return j;
    return -1;
  }
}
```

------------------------------------------------------------------------

# 🔄 Other Possible Approaches

1️⃣ Brute Force Permutation\
- Try all row permutations\
- Check validity each time\
- Complexity: O(n! \* n²)

2️⃣ Backtracking with Pruning\
- Slightly optimized brute\
- Still exponential

3️⃣ Greedy Row Selection (Current Solution) ✅\
- Compute suffix zeros\
- Bubble up valid row\
- Complexity: O(n²)

4️⃣ Counting Inversions Variant\
- Treat valid rows as sequence matching\
- Also O(n²) but more complex

------------------------------------------------------------------------

# 🔗 Related / Pattern Problems

-   https://leetcode.com/problems/minimum-swaps-to-make-strings-equal/
-   https://leetcode.com/problems/minimum-number-of-swaps-to-make-the-binary-string-alternating/
-   https://leetcode.com/problems/reorder-routes-to-make-all-paths-lead-to-the-city-zero/

Pattern Recognition: - Greedy placement - Counting adjacent swaps - Row
reordering constraint problems

------------------------------------------------------------------------

# 🧠 Interview Pattern Recognition

When you see:

✔ Matrix condition involving diagonal\
✔ Only adjacent row swaps allowed\
✔ Minimum swaps required

Think:

> "Can I convert this into a numeric requirement per row?"

That conversion step is the key trick.

------------------------------------------------------------------------

# 🎯 Memory Trick (Never Forget This)

Imagine:

Each row is a student standing in line. Each student must have enough
zeros behind them.

If a student doesn't qualify, bring the nearest qualified student
forward using bubble swaps.

💬 Repeat in your mind:

"Row i needs n-1-i zeros.\
Find it. Bubble it. Count it."

That's the entire problem.

------------------------------------------------------------------------

🔥 If you remember only one thing:

> Convert 2D constraint → 1D trailing zero requirement → Greedy bubble.

You will crack this instantly in interviews.
