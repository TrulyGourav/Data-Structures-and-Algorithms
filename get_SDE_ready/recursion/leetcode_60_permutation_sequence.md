
# 60. Permutation Sequence

🔗 LeetCode Link: https://leetcode.com/problems/permutation-sequence/

---

## Problem
The set [1, 2, 3, ..., n] contains a total of n! unique permutations.

By listing and labeling all of the permutations in order, we get the following sequence for n = 3:

123
132
213
231
312
321

Given n and k, return the kth permutation sequence.

Constraints:
- 1 <= n <= 9
- 1 <= k <= n!

---

## Intuition (MUST REMEMBER)
Instead of generating all permutations (which is expensive), we can directly find the kth permutation using factorial math.

Key idea:
For n numbers, total permutations = n!
Each digit position divides permutations into equal groups of size (n-1)!

Example:
n = 4 → 4! = 24 permutations
Each first digit repeats for 6 permutations (3!)

So:
index of first digit = k / (n-1)!

Repeat for remaining digits.

Think:
Permutation index behaves like number system with factorial base.

---

## Concept
Factorial Number System

Each position decides which unused number should be placed based on remaining permutations.

We maintain:
- list of available numbers
- factorial lookup
- convert k to zero based index

---

## Complexity
Time Complexity: O(n²)
Removing element from list costs O(n)

Space Complexity: O(n)

---

## Recursion Tree Visualization (n=3, k=3)

Numbers = [1,2,3]
k = 3 → zero index = 2

Level 1:
2 / 2! = 1 → pick index 1 → 2
Remaining = [1,3]

Level 2:
0 / 1! = 0 → pick 1
Remaining = [3]

Level 3:
pick 3

Result = 213

---

## Code (Java)

```java
class Solution {
  public String getPermutation(int n, int k) {
    StringBuilder sb = new StringBuilder();
    List<Integer> nums = new ArrayList<>();
    int[] fact = new int[n + 1];

    for (int i = 1; i <= n; ++i)
      nums.add(i);

    Arrays.fill(fact, 1);
    for (int i = 2; i <= n; ++i)
      fact[i] = fact[i - 1] * i;

    --k;

    for (int i = n - 1; i >= 0; --i) {
      int j = k / fact[i];
      k %= fact[i];

      sb.append(nums.get(j));
      nums.remove(j);
    }

    return sb.toString();
  }
}
```

---

## Other Approaches (Brute → Optimal)

1. Generate all permutations using recursion
Time: O(n!)
Space: O(n!)

2. Backtracking with visited array
Time: O(n!)
Space: O(n)

3. Next permutation k times
Time: O(k*n)

4. Factorial Number System (Optimal) ← CURRENT SOLUTION
Time: O(n²)
Space: O(n)

---

## Related Problems
Next Permutation
Permutations
Permutations II
Kth Smallest Element

---

## Pattern Recognition
When:
- kth arrangement
- kth permutation
- lexicographic order

Think:
factorial grouping

---

## Memory Tip
Each digit decides group of permutations.
Group size = factorial of remaining digits.

Formula:
index = k / factorial
