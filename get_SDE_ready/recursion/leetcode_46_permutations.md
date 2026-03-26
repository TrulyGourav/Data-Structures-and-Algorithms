
# 46. Permutations

🔗 LeetCode Link: https://leetcode.com/problems/permutations/

---

## Problem
Given an array nums of distinct integers, return all the possible permutations.

You can return the answer in any order.

Constraints:
- 1 <= nums.length <= 6
- -10 <= nums[i] <= 10
- All the integers of nums are unique

---

## Intuition (MUST REMEMBER)
Permutation problems usually mean:

"Try every number in every position"

At each step:
Pick one unused element
Place it in current position
Solve remaining problem recursively

Then backtrack:
Remove the chosen element
Try next possible candidate

Key thinking:
Choice → Explore → Undo choice → Explore next

Recursion builds the permutation step by step.

---

## Conceptual Understanding

This is a classic Backtracking problem.

We build permutation progressively.
At each recursion level:
we choose one unused element.

We maintain:
current path (partial permutation)
visited tracking
result list

Backtracking ensures we explore all possibilities.

---

## Complexity

Time Complexity: O(n * n!)
We generate n! permutations and each takes O(n) to copy.

Space Complexity: O(n)
Recursion depth is n.

---

## Recursion Tree Visualization

Example nums = [1,2,3]

                        []
            /             |             \
          [1]            [2]            [3]
        /     \       /     \       /     \
     [1,2]   [1,3] [2,1]   [2,3] [3,1]   [3,2]
      |        |      |       |      |        |
  [1,2,3] [1,3,2] [2,1,3] [2,3,1] [3,1,2] [3,2,1]

Each level fixes one position.

Depth = length of array

---

## Code (Java - Recursion + Backtracking)

```java
class Solution {

    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        boolean[] used = new boolean[nums.length];

        backtrack(nums, used, new ArrayList<>(), result);

        return result;
    }

    private void backtrack(int[] nums,
                           boolean[] used,
                           List<Integer> path,
                           List<List<Integer>> result) {

        if (path.size() == nums.length) {
            result.add(new ArrayList<>(path));
            return;
        }

        for (int i = 0; i < nums.length; i++) {

            if (used[i])
                continue;

            used[i] = true;
            path.add(nums[i]);

            backtrack(nums, used, path, result);

            path.remove(path.size() - 1);
            used[i] = false;
        }
    }
}
```

---

## Other Approaches (Brute → Optimal)

1. Generate permutations using library next_permutation repeatedly
Time: O(n! * n)

2. Recursion + extra array tracking
Time: O(n * n!)

3. Backtracking with swapping in-place
Time: O(n * n!)
Space: O(1)

4. Iterative BFS style building permutations
Time: O(n * n!)

5. Backtracking with boolean visited ← CURRENT SOLUTION
Time: O(n * n!)
Space: O(n)

---

## Related Problems

47. Permutations II (duplicates allowed)
31. Next Permutation
60. Permutation Sequence
77. Combinations
78. Subsets

---

## Pattern Recognition

When question says:
all permutations
all arrangements
all orderings

Think:
Backtracking

Choice tree grows factorially.

---

## Memory Tip

Permutation = Place each element at each position once.

Template to remember:

for every element:
    choose element
    explore deeper
    undo choice

CHOSE → EXPLORE → UNDO

Visualize tree levels = positions.
Each level reduces options.
