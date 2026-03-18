# 90. Subsets II

🔗 LeetCode Link: https://leetcode.com/problems/subsets-ii/

---

## 🧠 Problem Statement

Given an integer array `nums` that may contain duplicates, return all possible subsets (the power set).

The solution set must not contain duplicate subsets.

---

## 🌟 Intuition (MOST IMPORTANT)

The classic subsets problem gives us 2 choices for every element:
👉 Include it  
👉 Exclude it  

But here’s the twist:
🚨 Duplicate elements can create duplicate subsets.

💡 Key Idea:
- If we blindly include/exclude duplicates → duplicate subsets will be generated.
- So, **we must SKIP duplicates while making the "exclude" decision**.

👉 WHY skip during exclude?
Because:
- Include path already handles duplicates properly.
- Duplicate subsets mainly arise when we repeatedly exclude same values at same recursion level.

🔥 Rule to remember:
> “Sort first, and while excluding — skip all duplicates.”

---

## 🔍 Conceptual Understanding

1. Sort the array → duplicates come together
2. At every index:
   - Include current element
   - Backtrack
   - Skip all duplicates
   - Exclude

This ensures:
✔ Every subset is unique  
✔ No need for extra Set or Hashing  

---

## 🌳 Recursion Tree (Example: [1,2,2])

```
                          []
                   /              \
                [1]               []
              /     \          /     \
         [1,2]      [1]     [2]      []
         /   \               /   \
   [1,2,2] [1,2]        [2,2]   [2]
```

⚠ Notice:
Duplicate `2` is skipped during exclude branch.

---

## 🧮 Time & Space Complexity

| Complexity | Value |
|----------|------|
| Time     | O(2^n) |
| Space    | O(n) recursion stack + output |

---

## 💡 Code Solution (Java)

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(nums); // must
        findSubsets(nums, 0, new ArrayList<>(), ans);
        return ans;
    }

    public void findSubsets(int[] nums, int index, List<Integer> cur, List<List<Integer>> ans) {

        // Base case
        if (index == nums.length) {
            ans.add(new ArrayList<>(cur));
            return;
        }

        // Include current element
        cur.add(nums[index]);
        findSubsets(nums, index + 1, cur, ans);

        // Backtrack
        cur.remove(cur.size() - 1);

        // Skip duplicates before exclude
        while (index + 1 < nums.length && nums[index] == nums[index + 1]) {
            index++;
        }

        // Exclude current (after skipping duplicates)
        findSubsets(nums, index + 1, cur, ans);
    }
}
```

---

## 🧵 Other Approaches (Brute → Optimal)

1. Brute Force (Generate all subsets + Use Set)
   - Generate all subsets normally (2^n)
   - Store in Set to remove duplicates
   - Time: O(2^n * n)
   - Space: O(2^n)
   - ❌ Inefficient due to extra space

2. Bitmasking + Set
   - Use bitmask to generate subsets
   - Store in Set for uniqueness
   - Time: O(2^n * n)
   - Space: O(2^n)
   - ❌ Still uses extra space

3. Backtracking with Set
   - Generate subsets
   - Add to Set to avoid duplicates
   - ❌ Redundant storage

4. Optimized Backtracking (Current Solution) ✅
   - Sort array
   - Skip duplicates during recursion
   - Time: O(2^n)
   - Space: O(n)
   - ✔ Most optimal and clean

---

## 🔗 Related Problems

- Subsets (LeetCode 78) → https://leetcode.com/problems/subsets/
- Combination Sum II → https://leetcode.com/problems/combination-sum-ii/
- Permutations II → https://leetcode.com/problems/permutations-ii/

---

## 🎯 Pattern Recognition

👉 This is a **Backtracking + Duplicate Handling Pattern**

Whenever you see:
- "unique subsets"
- "no duplicate combinations"

Think:
✔ Sort the array  
✔ Skip duplicates  

---

## 🧠 MEMORY TIP (Never Forget This)

🔥 “INCLUDE freely, EXCLUDE carefully.”

OR

💡 “Duplicates hurt only when you IGNORE them during exclusion.”

OR even better:

👉 **“Sort → Include → Backtrack → Skip Duplicates → Exclude”**

If you remember this flow, you can solve:
- Subsets II
- Combination Sum II
- Permutations II

---

🚀 Master this pattern once, and you unlock multiple problems.
