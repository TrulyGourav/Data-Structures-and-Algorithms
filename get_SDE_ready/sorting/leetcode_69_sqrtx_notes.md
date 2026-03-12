# LeetCode 69 --- Sqrt(x)

**Problem Link:** https://leetcode.com/problems/sqrtx/

------------------------------------------------------------------------

## Problem Summary

Given a **non‑negative integer `x`**, return the **square root of `x`
rounded down to the nearest integer**.

You **cannot use built‑in exponent functions** such as:

-   `pow(x, 0.5)`
-   `x ** 0.5`

Example:

  Input   Output
  ------- --------
  x = 4   2
  x = 8   2

Explanation:\
√8 = 2.828..., and we return the **floor value → 2**.

------------------------------------------------------------------------

# Key Constraint

    0 ≤ x ≤ 2^31 − 1

Meaning:

    0 ≤ x ≤ 2147483647

This tells us:

-   `x` can be very large.
-   A **linear approach is inefficient**.

Therefore the expected optimal solution is **Binary Search**.

------------------------------------------------------------------------

# Core Intuition

We want the **largest integer `y` such that:**

    y² ≤ x

Instead of checking every number, we search using **Binary Search**.

Why binary search works:

-   The function `f(y) = y²` is **monotonically increasing**
-   Once `y²` exceeds `x`, all larger numbers will also exceed it.

So we can **discard half of the search space each step**.

------------------------------------------------------------------------

# Search Space

Possible square roots lie in:

    1 → x/2

(except when `x < 2`)

Example:

    x = 8
    √8 ≈ 2.828
    Answer = 2

------------------------------------------------------------------------

# Binary Search Approach

Steps:

1.  Define search range
2.  Compute mid
3.  Compare `mid²` with `x`
4.  Adjust range accordingly

Instead of:

    mid * mid > x

We use:

    mid > x / mid

This **avoids integer overflow**.

------------------------------------------------------------------------

# Java Implementation (Interview Friendly)

``` java
class Solution {

    public int mySqrt(int x) {

        if (x < 2) return x;

        int low = 1;
        int high = x / 2;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (mid == x / mid)
                return mid;

            if (mid > x / mid)
                high = mid - 1;
            else
                low = mid + 1;
        }

        return high;
    }
}
```

------------------------------------------------------------------------

# Complexity Analysis

### Time Complexity

    O(log x)

Because the search space halves each step.

Maximum steps when:

    x = 2^31

≈ **31 iterations**

------------------------------------------------------------------------

### Space Complexity

    O(1)

Only constant extra variables are used.

------------------------------------------------------------------------

# Example Walkthrough

Input:

    x = 8

Search Range:

    1 → 4

  low   high   mid   mid²   Action
  ----- ------ ----- ------ ------------
  1     4      2     4      move right
  3     4      3     9      move left

Loop ends:

    low = 3
    high = 2

Return:

    2

------------------------------------------------------------------------

# Interview Crux (What Interviewers Expect)

Important points to mention:

1.  Brute force solution exists but inefficient
2.  Binary search reduces complexity
3.  Use **overflow safe comparison**
4.  Return **high** when loop exits

This demonstrates:

-   Understanding of search patterns
-   Edge case handling
-   Integer overflow awareness

------------------------------------------------------------------------

# Edge Cases

  Input        Output
  ------------ --------
  0            0
  1            1
  2            1
  3            1
  2147395599   46339

------------------------------------------------------------------------

# Related LeetCode Problems

These problems use **binary search on answer space**.

### 1. Valid Perfect Square

https://leetcode.com/problems/valid-perfect-square/

### 2. Find Peak Element

https://leetcode.com/problems/find-peak-element/

### 3. Search Insert Position

https://leetcode.com/problems/search-insert-position/

### 4. First Bad Version

https://leetcode.com/problems/first-bad-version/

### 5. Koko Eating Bananas

https://leetcode.com/problems/koko-eating-bananas/

### 6. Capacity To Ship Packages Within D Days

https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/

------------------------------------------------------------------------

# Pattern Learned

This problem teaches the **Binary Search on Answer Pattern**.

Steps:

1.  Define search space
2.  Pick mid
3.  Validate mid
4.  Adjust search space
5.  Return best valid answer

------------------------------------------------------------------------

# Takeaway

Whenever a problem asks:

-   **minimum / maximum value**
-   **rounded down answer**
-   **large constraints**
-   **monotonic function**

Think:

    Binary Search on Answer
