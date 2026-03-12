# LeetCode 704 --- Binary Search

Problem Link: https://leetcode.com/problems/binary-search/

------------------------------------------------------------------------

## Problem Summary

Given a sorted array of integers `nums` and an integer `target`, return
the **index of target** if it exists in the array.

If the target does not exist, return **-1**.

The algorithm must run in **O(log n)** time.

------------------------------------------------------------------------

## Example

Input nums = \[-1,0,3,5,9,12\] target = 9

Output 4

Explanation: nums\[4\] = 9

------------------------------------------------------------------------

## Constraints

1 ≤ nums.length ≤ 10\^4\
-10\^4 \< nums\[i\], target \< 10\^4\
nums is sorted in **ascending order**

This strongly suggests using **Binary Search**.

------------------------------------------------------------------------

# Intuition

Because the array is sorted, we can eliminate half of the elements each
step.

Steps: 1. Look at the **middle element** 2. If it equals the target →
return index 3. If target is smaller → search left half 4. If target is
larger → search right half

------------------------------------------------------------------------

# Search Space

Initial range

0 → n-1

We repeatedly shrink the search range.

------------------------------------------------------------------------

# Safe Mid Formula

Always calculate mid like this:

mid = low + (high - low) / 2

This prevents **integer overflow**.

------------------------------------------------------------------------

# Java Solution

``` java
class Solution {
    public int search(int[] nums, int target) {

        int low = 0;
        int high = nums.length - 1;

        while (low <= high) {

            int mid = low + (high - low) / 2;

            if (nums[mid] == target) {
                return mid;
            }

            if (nums[mid] > target) {
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }

        return -1;
    }
}
```

------------------------------------------------------------------------

# Example Walkthrough

nums = \[-1,0,3,5,9,12\]\
target = 9

Step 1\
low = 0, high = 5\
mid = 2 → nums\[2\] = 3 → move right

Step 2\
low = 3, high = 5\
mid = 4 → nums\[4\] = 9 → found

Answer = **4**

------------------------------------------------------------------------

# Complexity Analysis

Time Complexity\
O(log n)

Binary search halves the search space every step.

Space Complexity\
O(1)

------------------------------------------------------------------------

# Edge Cases

target at first index → return 0\
target at last index → return n-1\
target not present → return -1\
single element array → check once

------------------------------------------------------------------------

# Interview Crux

Important things interviewers expect:

• Recognize sorted array → binary search\
• Use safe mid calculation\
• Correct loop condition: `while(low <= high)`\
• Return -1 when not found

------------------------------------------------------------------------

# Binary Search Template

low = 0\
high = n-1

while(low \<= high)

    mid = low + (high-low)/2

    if(nums[mid] == target)
        return mid

    if(nums[mid] > target)
        high = mid - 1
    else
        low = mid + 1

------------------------------------------------------------------------

# Related LeetCode Problems

Search Insert Position\
https://leetcode.com/problems/search-insert-position/

First Bad Version\
https://leetcode.com/problems/first-bad-version/

Find First and Last Position of Element\
https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/

Sqrt(x)\
https://leetcode.com/problems/sqrtx/

Koko Eating Bananas\
https://leetcode.com/problems/koko-eating-bananas/

------------------------------------------------------------------------

# Key Takeaway

Whenever you see:

Sorted array + searching element

Think immediately:

Binary Search
