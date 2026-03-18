# 78. Subsets

🔗 LeetCode Link: https://leetcode.com/problems/subsets/

---

## 🧠 Problem Statement

Given an integer array `nums` of **unique elements**, return all possible subsets (the power set).

The solution set must not contain duplicate subsets.

---

## 🌟 Intuition (MOST IMPORTANT)

👉 At every index, we have **2 choices**:
- Include the element
- Exclude the element

This is a classic **binary decision tree**:
```
For each element → Take it OR Skip it
```

So total subsets = `2^n`

---

## 🔍 Conceptual Understanding

This is a **Backtracking + Recursion** problem.

We explore all possibilities:
- Build subset step by step
- At each step, make a decision
- Backtrack to explore other possibilities

---

## 🌳 Recursion Tree (Example: [1,2])

```
                    []
                /        \
             [1]          []
           /    \       /    \
       [1,2]   [1]     [2]     []
```

---

## ⏱️ Time & Space Complexity

| Type | Complexity |
|------|------------|
| Time | O(2^n * n) |
| Space | O(n) recursion stack |

---

## 💡 Code Solution (Java)

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        findSubsets(nums, ans, new ArrayList<>(), 0);
        return ans;
    }

    public void findSubsets(int[] nums, List<List<Integer>> ans, List<Integer> curSubset, int index) {

        if (index == nums.length) {
            ans.add(new ArrayList<>(curSubset)); // store copy
            return;
        }

        curSubset.add(nums[index]);
        findSubsets(nums, ans, curSubset, index + 1);

        curSubset.remove(curSubset.size() - 1);

        findSubsets(nums, ans, curSubset, index + 1);
    }
}
```

---

## 🔄 Other Approaches (Brute → Optimal)

1. Bit Manipulation → O(2^n * n)
2. Iterative → O(2^n * n)
3. Backtracking (Current Solution) → O(2^n * n) ✅

---

## 🔗 Related Problems

- https://leetcode.com/problems/subsets-ii/
- https://leetcode.com/problems/permutations/

---

## 🎯 Pattern Recognition

- Subsets / Power Set
- Backtracking
- Decision Tree

---

## 🧠 Memory Tip

👉 “For every element → 2 choices → Include or Exclude”

Think like a switch: ON/OFF for each element.
