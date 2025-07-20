
# 🧮 2843. Count Symmetric Integers

## 📌 Problem Statement

You are given two **positive integers** `low` and `high`.

An integer `x` is called **symmetric** if:
- It has **even number of digits** (i.e., `2n` digits), and
- The **sum of the first `n` digits** is **equal to the sum of the last `n` digits**.

Return the **number of symmetric integers** in the **inclusive range** `[low, high]`.

> ❌ Integers with **odd number of digits** are never symmetric.

---

### 🧪 Examples

#### Example 1:
```
Input:  low = 1, high = 100  
Output: 9  
Explanation: Symmetric numbers: 11, 22, 33, 44, 55, 66, 77, 88, 99
```

#### Example 2:
```
Input:  low = 1200, high = 1230  
Output: 4  
Explanation: Symmetric numbers: 1203, 1212, 1221, 1230
```

---

## 💡 Intuition (Highlighted)

If we look closely, the **symmetric numbers always have even number of digits**, and the **sum of the first half = sum of second half**.

So instead of checking all numbers in brute force, we can optimize by:
- Skipping numbers with **odd digits** (e.g. 1, 100, 123).
- Extracting the **first and second halves** and comparing their digit sums.

💥 Core Insight:
> Symmetry here means **"balanced digit sums on both halves"**, not palindrome!

---

## 🧠 Conceptual Understanding

- Numbers like `1230` have 4 digits → split into `12` and `30`
- `sum(1 + 2) == sum(3 + 0) → 3 == 3` → ✅ Symmetric

Key points:
- Ignore all numbers with odd digit count
- Split the digits in half
- Compare digit sums

---

## 🧭 Approach

1. **Iterate** through numbers from `low` to `high`
2. For each number:
   - Check if the digit count is even
   - Divide number into two halves
   - Sum digits of each half
   - Compare sums
3. If equal → count as symmetric

---

## ⏱️ Time and Space Complexity

| Complexity | Value         |
|------------|---------------|
| 🕰️ Time     | O(N * D) where D is number of digits (max 5) |
| 🧠 Space    | O(1) – no extra space used |

---

## ✅ Code Solution (Java)

```java
class Solution {
  public int countSymmetricIntegers(int low, int high) {
    int ans = 0;

    for (int num = low; num <= high; ++num)
      if (isSymmetricInteger(num))
        ++ans;

    return ans;
  }

  private boolean isSymmetricInteger(int num) {
    if (num >= 10 && num <= 99)
      return num / 10 == num % 10;

    if (num >= 1000 && num <= 9999) {
      final int left = num / 100;
      final int right = num % 100;
      return left / 10 + left % 10 == right / 10 + right % 10;
    }

    return false;
  }
}
```

---

## 🔁 All Approaches Comparison

| Approach | Description | Time | Space | Status |
|---------|-------------|------|-------|--------|
| Brute Force | Check all numbers, split digits, check sum | O(N * D) | O(D) | ⚪️ |
| Filter even-digit numbers + string split | Convert to string, split halves, sum digits | O(N * D) | O(D) | ⚪️ |
| Integer math (used above) | Use integer division/modulus to split and compare halves | O(N) | O(1) | ✅ (Current) |

---

## 🧠 Pattern Recognition & Similar Problems

| Pattern | Related Problems |
|--------|------------------|
| Digit Sum / Math Tricks | 🔹 [Add Digits](https://leetcode.com/problems/add-digits) <br> 🔹 [Sum of Digits in Base K](https://leetcode.com/problems/sum-of-digits-in-base-k) |
| Number Property Scanning | 🔹 [Palindrome Number](https://leetcode.com/problems/palindrome-number) <br> 🔹 [Armstrong Numbers (Coding Ninjas)] |

This problem helps reinforce the **digit processing pattern** — useful for numerical digit-based logic.

---

## 🧠 How to Never Forget This?

### 🎯 Tip to Remember:
> Think of the number as a **digit seesaw** – both halves need to be **balanced** to stay symmetric!

Visual:
```
If 4-digit number = AB | CD, then:
  A + B  ==  C + D   →  symmetric!

Same logic applies for 2n-digit numbers in general.
```

🔥 Pro Tip: Memorize the fact that:
- 2-digit symmetric = repeated digits: `11, 22, ...`
- 4-digit symmetric = digit sum halves equal

So in an interview, remember:
> "Is this number *digitally balanced* on both sides?"
