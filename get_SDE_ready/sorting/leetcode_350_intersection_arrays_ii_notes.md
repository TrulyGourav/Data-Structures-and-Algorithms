# LeetCode 350 --- Intersection of Two Arrays II

Problem Link:
https://leetcode.com/problems/intersection-of-two-arrays-ii/

------------------------------------------------------------------------

## Problem Summary

Given two integer arrays `nums1` and `nums2`, return an array of their
intersection.

Each element in the result must appear as many times as it shows in both
arrays.

You may return the result in any order.

------------------------------------------------------------------------

## Example

Input: nums1 = \[1,2,2,1\] nums2 = \[2,2\]

Output: \[2,2\]

Explanation: 2 appears twice in both arrays.

------------------------------------------------------------------------

# Intuition

We need to capture duplicates that appear in **both arrays**.

A good approach:

1.  Sort both arrays
2.  Use two pointers
3.  Traverse arrays together

Sorting allows us to compare elements efficiently.

------------------------------------------------------------------------

# Core Idea

After sorting:

nums1 = \[1,1,2,2\]\
nums2 = \[2,2\]

We move two pointers:

i → nums1\
j → nums2

If elements match → add to result.

------------------------------------------------------------------------

# Two Pointer Logic

Case 1:

nums1\[i\] == nums2\[j\]

Add element to result and move both pointers.

Case 2:

nums1\[i\] \< nums2\[j\]

Move pointer `i`.

Case 3:

nums1\[i\] \> nums2\[j\]

Move pointer `j`.

------------------------------------------------------------------------

# Java Implementation

``` java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {

        Arrays.sort(nums1);
        Arrays.sort(nums2);

        int l1 = nums1.length;
        int l2 = nums2.length;

        int i = 0, j = 0, k = 0;

        while(i < l1 && j < l2){

            if(nums1[i] == nums2[j]){
                nums1[k] = nums2[j];
                k++;
                i++;
                j++;
            }
            else if(nums1[i] < nums2[j]){
                i++;
            }
            else{
                j++;
            }
        }

        return Arrays.copyOfRange(nums1, 0, k);
    }
}
```

------------------------------------------------------------------------

# Example Walkthrough

nums1 = \[1,2,2,1\]\
nums2 = \[2,2\]

After sorting:

nums1 = \[1,1,2,2\]\
nums2 = \[2,2\]

  i   j   nums1\[i\]   nums2\[j\]   Action
  --- --- ------------ ------------ --------
  0   0   1            2            move i
  1   0   1            2            move i
  2   0   2            2            add 2
  3   1   2            2            add 2

Result:

\[2,2\]

------------------------------------------------------------------------

# Complexity Analysis

Time Complexity:

O(n log n + m log m)

Because we sort both arrays.

n = length of nums1\
m = length of nums2

------------------------------------------------------------------------

Space Complexity:

O(1)

We reuse nums1 for storing the result.

------------------------------------------------------------------------

# Alternative Approach (HashMap)

Another common solution:

1.  Store frequency of elements in nums1
2.  Iterate nums2
3.  Decrease frequency when match found

Time:

O(n + m)

Space:

O(n)

------------------------------------------------------------------------

# When To Use Which Approach

Sorting + Two Pointer Good when arrays are already sorted.

HashMap Good when arrays are unsorted and extra space is allowed.

------------------------------------------------------------------------

# Edge Cases

nums1 = \[\] → return \[\]

nums2 = \[\] → return \[\]

nums1 = \[1,1,1\], nums2 = \[1,1\]

Output:

\[1,1\]

------------------------------------------------------------------------

# Related LeetCode Problems

Intersection of Two Arrays\
https://leetcode.com/problems/intersection-of-two-arrays/

Two Sum\
https://leetcode.com/problems/two-sum/

Merge Sorted Array\
https://leetcode.com/problems/merge-sorted-array/

------------------------------------------------------------------------

# Pattern Learned

Sorting + Two Pointer Pattern

Steps:

1.  Sort arrays
2.  Use two pointers
3.  Compare elements
4.  Move pointers strategically

------------------------------------------------------------------------

# Key Takeaway

Whenever you see:

-   Two arrays
-   Need common elements
-   Duplicates allowed

Think:

Sorting + Two Pointer.
