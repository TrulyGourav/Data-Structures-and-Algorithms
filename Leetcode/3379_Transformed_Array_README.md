# 🚀 3379. Transformed Array (Easy)

------------------------------------------------------------------------

## 📌 Problem Statement

You are given an integer array `nums` that represents a **circular
array**.

Your task is to create a new array `result` of the same size, following
these rules:

For each index `i` (where `0 <= i < nums.length`):

-   If `nums[i] > 0`:\
    Start at index `i` and move `nums[i]` steps to the **right** in the
    circular array.\
    Set `result[i]` to the value at the index where you land.

-   If `nums[i] < 0`:\
    Start at index `i` and move `abs(nums[i])` steps to the **left** in
    the circular array.\
    Set `result[i]` to the value at the index where you land.

-   If `nums[i] == 0`:\
    Set `result[i] = nums[i]`.

Since the array is circular: - Moving past the last element wraps to the
beginning. - Moving before the first element wraps to the end.

------------------------------------------------------------------------

# 🌟 Core Intuition (MOST IMPORTANT PART)

🔥 **Key Realization:**\
Instead of physically moving left or right step-by-step, we can directly
calculate the final index mathematically using modulo arithmetic.

The circular behavior can be handled using:

    (i + nums[i]) % n

But this alone is NOT enough because:

-   Java modulo with negative numbers gives negative results.
-   We must always ensure index stays within `[0, n-1]`.

So we normalize it safely using:

    (i + nums[i] % n + n) % n

💡 Why this works:

-   `nums[i] % n` → reduces unnecessary large jumps.
-   `+ n` → prevents negative values.
-   `% n` → ensures circular wrapping.

👉 Instead of simulating movement, we compute destination in O(1).

That's the entire trick.

------------------------------------------------------------------------

# 🧠 Conceptual Understanding

This problem is purely about:

-   Circular array handling
-   Modulo arithmetic normalization
-   Avoiding brute force movement

The movement can be visualized like this:

Example:

    nums = [2, -1, 1]
    n = 3

    Index 0:
    Move 2 right → (0 + 2) % 3 = 2
    result[0] = nums[2]

    Index 1:
    Move 1 left → (1 - 1) = 0
    result[1] = nums[0]

    Index 2:
    Move 1 right → (2 + 1) % 3 = 0
    result[2] = nums[0]

------------------------------------------------------------------------

# 🌳 Circular Movement Visualization

Example:

    nums = [3, -2, 0, 1]
    n = 4

                0
             /     \
            3       1
             \     /
                2

    For i = 1 (nums[1] = -2):

    Start at 1
    Move left 2 steps:

    1 -> 0 -> 3

    Landing index = 3

Formula handles this automatically:

    newIndex = (i + nums[i] % n + n) % n

------------------------------------------------------------------------

# 🧮 Time & Space Complexity

  Complexity   Value
  ------------ -------
  Time         O(n)
  Space        O(n)

-   Single loop → O(n)
-   Result array → O(n)
-   No extra data structures

------------------------------------------------------------------------

# 💻 Code Solution (Optimal)

``` java
class Solution {
  public int[] constructTransformedArray(int[] nums) {
    final int n = nums.length;
    int[] ans = new int[n];

    for (int i = 0; i < n; ++i)
      ans[i] = nums[(i + nums[i] % n + n) % n];

    return ans;
  }
}
```

------------------------------------------------------------------------

# 🧵 Other Possible Approaches (Brute → Optimal)

1️⃣ Brute Force Simulation\
- For each index, move step-by-step left or right.\
- Time: O(n²)\
- Space: O(n)

2️⃣ While Loop Simulation\
- Same idea but cleaner simulation logic.\
- Time: O(n²)\
- Space: O(n)

3️⃣ Mathematical Modulo Approach ✅ (Current Optimal Solution)\
- Direct index calculation\
- Time: O(n)\
- Space: O(n)

------------------------------------------------------------------------

# 🔗 Related Problems (Pattern Reinforcement)

1.  Rotate Array (LeetCode 189)
2.  Circular Array Loop (LeetCode 457)
3.  Defuse the Bomb (LeetCode 1652)
4.  Next Greater Element II (LeetCode 503)

These strengthen circular array + modulo thinking.

------------------------------------------------------------------------

# 🎯 Pattern Recognition

If you see: - Circular array - Moving steps left or right - Wrap-around
behavior

Immediately think:

👉 **Modulo Arithmetic** 👉 Normalize negative index using +n 👉 Final
formula: (index + steps % n + n) % n

------------------------------------------------------------------------

# 🧠 Never Forget This Trick (Memory Hack)

Whenever you see circular movement:

Imagine a clock 🕒

-   Moving right = clockwise
-   Moving left = anticlockwise
-   Clock never goes negative
-   After 12 comes 1 again

So always remember:

"Clock logic = Modulo logic"

Final Formula Mantra:

👉 ADD → MOD → NORMALIZE → MOD

    (i + nums[i] % n + n) % n

If you remember this one formula, you'll never struggle with circular
arrays again.

------------------------------------------------------------------------

🔥 This problem is easy, but the modulo normalization trick is extremely
powerful for interviews.

Master this --- and circular array questions become free marks.
