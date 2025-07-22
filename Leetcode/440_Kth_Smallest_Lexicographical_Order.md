# 440. K-th Smallest in Lexicographical Order

## 🧾 Problem Statement

You are given two integers `n` and `k`. Your task is to **find the k-th smallest number** in **lexicographical order** in the range `[1, n]`.

### 🔸 Examples:

#### Example 1:
```
Input: n = 13, k = 2
Output: 10

Explanation:
Lexicographical Order: [1, 10, 11, 12, 13, 2, 3, 4, 5, 6, 7, 8, 9]
→ The 2nd number is 10.
```

#### Example 2:
```
Input: n = 1, k = 1
Output: 1
```

### 🧾 Constraints:
- 1 ≤ k ≤ n ≤ 10⁹

---

## 🌟 Intuition (Must-Understand)

Think of the numbers in lexicographical order as nodes in a **prefix tree (trie)**. The root starts at `1`, and each number has children formed by appending digits (0–9) if they are ≤ `n`.

```
Visual Tree for n = 13
                  1
         /  /  /  |   \
       10 11 12 13  ...
      /
     100 (too big > 13 → prune)
```

- We **navigate** this tree using DFS-like logic, but **count** how many numbers exist under a given prefix.
- If the count under the current prefix is less than `k`, we **skip that subtree** and move to the next prefix.
- If the count is ≥ `k`, we **go deeper into that subtree**.

---

## 🔍 Conceptual Understanding

- **Lexicographical order** is how words are ordered in a dictionary.
- Imagine numbers are strings: `"1", "10", "100", ..., "2", "3", ..."`
- You do not generate the entire list (which is impossible for n=10⁹), instead you **count the nodes** in each subtree.

---

## ⏱️ Time and Space Complexity

| Approach             | Time Complexity          | Space Complexity |
|----------------------|--------------------------|------------------|
| Optimized Prefix Tree Counting | O(log(n)²)                | O(1)              |

---

## 🌳 Recursion Tree / Graph View (Centered)

Take `n = 13`, `k = 2`

```
                         "1"
                        / | \
                    "10" "11" "12" ...
                        |
                      "100" (pruned > n)
```

**Start at prefix = 1**  
- Count all numbers starting with "1" → 1,10,11,12,13 → count = 5  
- Since 5 >= k (2), go deeper:
  - Now prefix = 10 → 10 → count = 1  
  - We've found the second element.

**Answer = 10**

---

## ✅ Code: Java

```java
class Solution {
    public int findKthNumber(int n, int k) {
        int curr = 1;
        k--; // because we already consider 1 as first

        while (k > 0) {
            long steps = countSteps(n, curr, curr + 1);
            if (steps <= k) {
                k -= steps;
                curr++; // move to next sibling
            } else {
                curr *= 10; // go to first child
                k--; // move one step down
            }
        }

        return curr;
    }

    private long countSteps(int n, long first, long last) {
        long steps = 0;
        while (first <= n) {
            steps += Math.min(n + 1L, last) - first;
            first *= 10;
            last *= 10;
        }
        return steps;
    }
}
```

---

## 🧵 Other Possible Approaches

| Approach                    | Complexity       | Note |
|-----------------------------|------------------|------|
| Brute-force (Generate all, sort) | O(n log n)     | ❌ TLE for large n |
| BFS traversal over Trie     | O(n)             | ❌ Too slow for large n |
| **Optimized Prefix-Counting (Current)** | **O(log² n)** | ✅ Best for 1 ≤ n ≤ 10⁹ |

---

## 🔗 Related / Associated Problems

| Problem | Link |
|--------|------|
| Lexicographical Numbers | [LeetCode 386](https://leetcode.com/problems/lexicographical-numbers/) |
| K-th Smallest Element in Sorted Matrix | [LeetCode 378](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/) |
| K-th Symbol in Grammar | [LeetCode 779](https://leetcode.com/problems/k-th-symbol-in-grammar/) |

---

## 🧠 Pattern Recognition

- Lexicographical traversal = Preorder traversal of a **prefix tree**
- Trie-like structure helps in solving massive range problems efficiently
- Skip subtrees based on **number of descendants**
- Similar to binary search on implicit tree structures

---

## 🧠 Memory Tip: Never Forget This Logic

🔑 Think of numbers as **strings** and visualize a **dictionary traversal**.

- Imagine `k-th` means: _walk through this dictionary until we reach the `k-th` word_
- Use "skip over subtrees" when possible, else "go deeper"
- The `countSteps()` function is your way of **jumping** over entire chunks.

🗣️ **Analogy**:
> You're flipping through a dictionary. If the section starting with "1" has 5 pages and you're looking for the 7th word, you flip the entire "1" section and go to "2".  
> But if you're looking for the 2nd word, you zoom into the "1" section, deeper and deeper.

💭 Tip:
> Remember `Trie + Skip Counting` — if you can count how many lie beneath a prefix, you can navigate the tree **without building it**!

---

```
🔥 FAANG Tip:
This problem tests your ability to think beyond arrays and into implicit tree structures. It's a favorite for testing depth in logic, recursion avoidance, and prefix manipulation.
```

---

```
🧑‍💻 Prepared by: Your GitHub Handle
📁 Add this to your: /DSA/Trie/ or /DSA/PrefixTraversal/ folder
```