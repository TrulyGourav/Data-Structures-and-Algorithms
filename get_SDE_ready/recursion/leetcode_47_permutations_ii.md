
# 47. Permutations II

🔗 LeetCode Link: https://leetcode.com/problems/permutations-ii/

---

## Problem
Given a collection of numbers, nums, that might contain duplicates, return all possible unique permutations in any order.

Constraints:
- 1 <= nums.length <= 8
- -10 <= nums[i] <= 10

Example:
Input: nums = [1,1,2]
Output:
[
 [1,1,2],
 [1,2,1],
 [2,1,1]
]

---

# Intuition (VERY IMPORTANT)
Duplicates cause repeated permutations.

If we blindly generate permutations → duplicate answers.

So we:
1. Sort array first
2. Skip duplicate numbers during recursion
3. Only use duplicate if previous identical number is already used in same recursion branch

Key thought:
Same numbers should not start permutation at same tree level more than once.

---

# Concept
Backtracking + duplicate control

Rules:
Use visited array
Sort input
Skip duplicates using condition:

if(i>0 && nums[i]==nums[i-1] && !visited[i-1])
    continue;

Meaning:
Use duplicate only if previous duplicate already used

---

# Complexity
Time Complexity: O(n!)
Space Complexity: O(n)

Because maximum permutations = 8!

---

# Recursion Tree Example (nums=[1,1,2])

Sorted input:
[1,1,2]

Level 0:
        []
       /        1    2
     /
    1
   /
  2

Unique permutations formed:
112
121
211

Duplicate branches pruned early

---

# Code (Java Recursive Accepted Solution)

```java
class Solution {

    public List<List<Integer>> permuteUnique(int[] nums) {

        Arrays.sort(nums);

        List<List<Integer>> result = new ArrayList<>();

        boolean[] visited = new boolean[nums.length];

        backtrack(nums, visited, new ArrayList<>(), result);

        return result;
    }

    private void backtrack(int[] nums,
                           boolean[] visited,
                           List<Integer> current,
                           List<List<Integer>> result){

        if(current.size() == nums.length){

            result.add(new ArrayList<>(current));
            return;
        }

        for(int i=0;i<nums.length;i++){

            if(visited[i])
                continue;

            if(i>0 && nums[i]==nums[i-1] && !visited[i-1])
                continue;

            visited[i] = true;

            current.add(nums[i]);

            backtrack(nums, visited, current, result);

            current.remove(current.size()-1);

            visited[i] = false;
        }
    }
}
```

---

# Other Approaches (Brute → Optimal)

1. Generate all permutations and store in Set
Time: O(n!*n)
Space: O(n!*n)

2. Swap based permutation + Set duplicate removal
Time: O(n!*n)

3. Backtracking + sorting + skip duplicates (Optimal) ← CURRENT SOLUTION
Time: O(n!)
Space: O(n)

---

# Related Problems
46. Permutations
31. Next Permutation
60. Permutation Sequence
77. Combinations
78. Subsets

---

# Pattern Recognition

When problem says:
- all permutations
- unique permutations
- duplicates present

Think:
Backtracking + duplicate skipping

Template:
sort + visited + skip condition

---

# Memory Tip

Duplicates are dangerous at same tree level.

Rule:
Only pick duplicate if previous duplicate already used in path.

Sentence to remember:

"Same number cannot start branch twice at same level"
