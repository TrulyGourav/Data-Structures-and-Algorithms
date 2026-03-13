# LeetCode 1351 --- Count Negative Numbers in a Sorted Matrix

Problem Link:
https://leetcode.com/problems/count-negative-numbers-in-a-sorted-matrix/

------------------------------------------------------------------------

## Problem Summary

You are given an m x n matrix `grid` where: - Each row is sorted in
**non-increasing order** - Each column is sorted in **non-increasing
order**

Your task is to count the **total number of negative numbers** in the
matrix.

Example:

Input: grid = \[\[4,3,2,-1\], \[3,2,1,-1\], \[1,1,-1,-2\],
\[-1,-1,-2,-3\]\]

Output: 8

------------------------------------------------------------------------

## Key Observation

Rows are sorted decreasingly:

\[ 5 3 2 -1 -2 \] \[ 4 2 1 -1 -3 \] \[ 3 1 -1 -2 -5 \]

Once we encounter the **first negative element in a row**, all elements
to the right are also negative.

So we only need to **find the boundary where negatives start**.

------------------------------------------------------------------------

## Core Intuition

For each row:

1.  Use Binary Search
2.  Find the **first negative element**
3.  Count elements to the right

negatives in row = cols - firstNegativeIndex

Add this for all rows.

------------------------------------------------------------------------

## Binary Search Strategy

Search range in each row:

0 → cols-1

Conditions:

grid\[mid\] ≥ 0 → move right\
grid\[mid\] \< 0 → move left

Goal: find the **first negative number**.

------------------------------------------------------------------------

## Java Solution

``` java
class Solution {
    public int countNegatives(int[][] grid) {
        int ans = 0;
        int rows = grid.length;
        int cols = grid[0].length;

        for(int i=0; i<rows; i++){
            int start = 0;
            int end = cols-1;

            while(start <= end){
                int mid = start + (end-start)/2;

                if(grid[i][mid] >= 0){
                    start = mid+1;
                } else {
                    end = mid-1;
                }
            }

            ans += (cols-start);
        }

        return ans;
    }
}
```

------------------------------------------------------------------------

## Example Walkthrough

Row:

\[4, 3, 2, -1\]

Binary search finds:

first negative index = 3

Count:

4 - 3 = 1

------------------------------------------------------------------------

## Complexity

Time Complexity:

O(m log n)

Binary search for each row.

Space Complexity:

O(1)

------------------------------------------------------------------------

## Even Better Approach

You can solve this in:

O(m + n)

Start from **bottom-left** of the matrix.

Rules:

negative → move right\
positive → move up

Each move eliminates a row or column.

------------------------------------------------------------------------

## Edge Cases

All positive → answer = 0\
All negative → answer = m \* n\
Single row / column → simple traversal

------------------------------------------------------------------------

## Pattern Learned

Binary Search on sorted rows.

Find boundary where condition changes.

------------------------------------------------------------------------

## Related LeetCode Problems

Search Insert Position\
https://leetcode.com/problems/search-insert-position/

First Bad Version\
https://leetcode.com/problems/first-bad-version/

Find First and Last Position in Sorted Array\
https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/

Valid Perfect Square\
https://leetcode.com/problems/valid-perfect-square/

Sqrt(x)\
https://leetcode.com/problems/sqrtx/
