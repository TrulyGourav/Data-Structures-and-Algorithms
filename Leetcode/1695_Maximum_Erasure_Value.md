# 🧠 1695. Maximum Erasure Value

### 🔗 Problem Link: [LeetCode - 1695](https://leetcode.com/problems/maximum-erasure-value/)

---

## 🧾 Problem Statement

You are given an array of **positive integers** `nums` and want to **erase** a subarray containing **unique elements**. The score you get by erasing the subarray is **equal to the sum** of its elements.

Return the **maximum score** you can get by erasing **exactly one subarray**.

> A subarray is a contiguous part of an array.

---

## 🧩 Example

### Example 1:
```
Input:  nums = [4,2,4,5,6]  
Output: 17  
Explanation: The optimal subarray is [2,4,5,6].
```

### Example 2:
```
Input:  nums = [5,2,1,2,5,2,1,2,5]  
Output: 8  
Explanation: The optimal subarray is [5,2,1] or [1,2,5].
```

---

## 💡 Intuition (🤖 Human Way of Thinking)

Imagine you're **walking through the array** and collecting numbers in your bag (a subarray).  
Every time you see a **number you already have in your bag**, you must **drop items from the start** until that duplicate is gone – because your bag must contain **unique items only**.

As you're walking:
- You're **tracking the sum** of what's in your bag.
- You're also **keeping track of the maximum sum** you've ever had during this process.

This is a classic **sliding window problem**, where the window **shrinks or expands** depending on duplicates.  
The trick is to move the **left boundary forward** when you hit a duplicate.

---

## 🛠️ Approach: Sliding Window + HashSet

We maintain:
- A **sliding window** using two pointers (`left`, `right`)
- A `HashSet` to keep track of **unique elements** in the window
- A `currentSum` to track the sum of the current unique subarray
- A `maxSum` to track the best score seen so far

---

## ⌛ Time and Space Complexity

| Complexity | Value |
|-----------|-------|
| Time      | O(N), since each element is added and removed from the set at most once |
| Space     | O(N), due to the HashSet storing unique elements |

---

## 🔍 Conceptual Understanding

This is based on the **"longest substring without repeating characters"** pattern – but instead of just length, we **sum the values** of elements.

---

## 🌳 Recursion Tree Visualization (Conceptual Sliding Window Flow)

Consider this input: `[4, 2, 4, 5, 6]`

```
Start         [4]               sum = 4
Expand        [4,2]             sum = 6
Duplicate     [4,2,4] ❌ 4 exists, slide left
Shrink        [2,4]             sum = 6
Expand        [2,4,5]           sum = 11
Expand        [2,4,5,6]         sum = 17 ✅ max
```

At each step, we’re either:
- **Expanding** the window when unique
- **Shrinking** it from the left if duplicate appears

---

## ✅ Code Solution (Optimal Sliding Window)

```java
class Solution {
    public int maximumUniqueSubarray(int[] nums) {
        Set<Integer> seen = new HashSet<>();
        int left = 0, right = 0;
        int currentSum = 0, maxSum = 0;

        while (right < nums.length) {
            if (!seen.contains(nums[right])) {
                seen.add(nums[right]);
                currentSum += nums[right];
                maxSum = Math.max(maxSum, currentSum);
                right++;
            } else {
                seen.remove(nums[left]);
                currentSum -= nums[left];
                left++;
            }
        }

        return maxSum;
    }
}
```

---

## 🧠 Other Possible Solutions (Approaches & Complexities)

| Approach                 | Description                                                               | Time       | Space      |
|--------------------------|---------------------------------------------------------------------------|------------|------------|
| Brute Force              | Try all subarrays and check if all elements are unique                   | O(N^2)     | O(N)       |
| HashMap + PrefixSum      | Use HashMap to track last indices and adjust sum with prefix tricks      | O(N)       | O(N)       |
| ✅ Sliding Window (used) | Track unique elements with HashSet, maintain window and rolling sum      | O(N)       | O(N)       |

---

## 🧩 Related Problems

- [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) *(Very similar pattern)*
- [3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- [1208. Get Equal Substrings Within Budget](https://leetcode.com/problems/get-equal-substrings-within-budget/)
- [1004. Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/)

---

## 🧠 Pattern Recognition

This is a **Sliding Window + HashSet** pattern.  
Learn to:
- Expand window while condition is valid
- Shrink when duplicate/violation occurs
- Maintain auxiliary data like sum or length

---

## 🧠 Tip to Remember This Logic Forever

🧠 **"Like collecting gems in a bag — if I see a gem again, I throw out the earliest one until it’s unique again."**

Or imagine:
> You're collecting unique Pokémon cards on a walk. If you see a repeat, throw away cards starting from the oldest until your set is unique again — and track the most valuable combo.

**🎯 Sliding Window + Set + Rolling Sum = Max Score on Unique Path**

---
