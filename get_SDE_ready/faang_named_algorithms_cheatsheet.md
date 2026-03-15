# FAANG DSA -- Named Algorithms Cheat Sheet

This document lists important **algorithms named after people** that
frequently appear in FAANG‑level preparation.

Each section includes: - Purpose - Why it matters - Related LeetCode
practice

------------------------------------------------------------------------

# 1. Searching & Selection

## Quickselect (Tony Hoare)

**Purpose** Find kth smallest/largest element using quicksort partition
idea.

**Importance** Average O(n) selection algorithm.

**LeetCode**
https://leetcode.com/problems/kth-largest-element-in-an-array/

------------------------------------------------------------------------

## Median of Medians (BFPRT)

**Purpose** Deterministic selection algorithm.

**Importance** Guarantees O(n) worst‑case selection.

**Practice**
https://leetcode.com/problems/kth-largest-element-in-an-array/

------------------------------------------------------------------------

# 2. Sorting Algorithms

## Quicksort (Tony Hoare)

**Purpose** Divide‑and‑conquer sorting algorithm.

**Importance** Most commonly used fast sorting algorithm.

**LeetCode** https://leetcode.com/problems/sort-an-array/

------------------------------------------------------------------------

## Heapsort (J. W. J. Williams)

**Purpose** Sort using heap structure.

**Importance** O(n log n) guaranteed.

**LeetCode**
https://leetcode.com/problems/kth-largest-element-in-an-array/

------------------------------------------------------------------------

## Timsort (Tim Peters)

**Purpose** Hybrid merge + insertion sort.

**Importance** Used internally in Python and Java.

------------------------------------------------------------------------

# 3. Graph Algorithms

## Dijkstra's Algorithm

**Purpose** Find shortest path in graphs with non‑negative weights.

**Importance** Most common shortest path algorithm.

**LeetCode** https://leetcode.com/problems/network-delay-time/

------------------------------------------------------------------------

## Bellman--Ford Algorithm

**Purpose** Shortest path with negative weights.

**Importance** Detects negative cycles.

**LeetCode**
https://leetcode.com/problems/cheapest-flights-within-k-stops/

------------------------------------------------------------------------

## Floyd--Warshall Algorithm

**Purpose** All pairs shortest path.

**Importance** Useful for dense graphs.

**LeetCode**
https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/

------------------------------------------------------------------------

## Kruskal's Algorithm

**Purpose** Minimum spanning tree using union‑find.

**Importance** Classic greedy MST algorithm.

**LeetCode**
https://leetcode.com/problems/min-cost-to-connect-all-points/

------------------------------------------------------------------------

## Prim's Algorithm

**Purpose** Another MST algorithm using priority queue.

**LeetCode**
https://leetcode.com/problems/min-cost-to-connect-all-points/

------------------------------------------------------------------------

## Tarjan's Algorithm

**Purpose** Find strongly connected components.

**LeetCode**
https://leetcode.com/problems/critical-connections-in-a-network/

------------------------------------------------------------------------

## Kosaraju's Algorithm

**Purpose** Strongly connected components using two DFS passes.

------------------------------------------------------------------------

## Kahn's Algorithm

**Purpose** Topological sort using indegree.

**LeetCode** https://leetcode.com/problems/course-schedule/

------------------------------------------------------------------------

# 4. String Algorithms

## Knuth‑Morris‑Pratt (KMP)

**Purpose** Efficient substring search.

**Importance** Avoids repeated comparisons.

**LeetCode**
https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/

------------------------------------------------------------------------

## Rabin‑Karp

**Purpose** String matching using rolling hash.

**LeetCode** https://leetcode.com/problems/repeated-string-match/

------------------------------------------------------------------------

## Boyer‑Moore

**Purpose** Fast practical string searching.

------------------------------------------------------------------------

## Manacher's Algorithm

**Purpose** Longest palindromic substring in O(n).

**LeetCode**
https://leetcode.com/problems/longest-palindromic-substring/

------------------------------------------------------------------------

# 5. Dynamic Programming

## Kadane's Algorithm

**Purpose** Maximum subarray sum.

**LeetCode** https://leetcode.com/problems/maximum-subarray/

------------------------------------------------------------------------

# 6. Number Theory

## Euclidean Algorithm

**Purpose** Compute greatest common divisor.

**LeetCode**
https://leetcode.com/problems/find-greatest-common-divisor-of-array/

------------------------------------------------------------------------

## Sieve of Eratosthenes

**Purpose** Generate prime numbers up to n.

**LeetCode** https://leetcode.com/problems/count-primes/

------------------------------------------------------------------------

## Miller‑Rabin Primality Test

**Purpose** Fast probabilistic prime testing.

------------------------------------------------------------------------

# 7. Bit Manipulation

## Brian Kernighan's Algorithm

**Purpose** Count number of set bits.

Core idea:

n = n & (n - 1)

**LeetCode** https://leetcode.com/problems/number-of-1-bits/

------------------------------------------------------------------------

## Gray Code (Frank Gray)

**Purpose** Generate sequence differing by one bit.

**LeetCode** https://leetcode.com/problems/gray-code/

------------------------------------------------------------------------

# 8. Data Structures Named After People

## AVL Tree

**Purpose** Self balancing binary search tree.

------------------------------------------------------------------------

## Fenwick Tree (Binary Indexed Tree)

**Purpose** Efficient prefix sums and updates.

**LeetCode** https://leetcode.com/problems/range-sum-query-mutable/

------------------------------------------------------------------------

## Red‑Black Tree

**Purpose** Balanced BST used in many standard libraries.

------------------------------------------------------------------------

# 9. Randomized Algorithms

## Fisher‑Yates Shuffle

**Purpose** Generate unbiased random shuffle.

**LeetCode** https://leetcode.com/problems/shuffle-an-array/

------------------------------------------------------------------------

## Reservoir Sampling

**Purpose** Random sampling from streaming data.

**LeetCode** https://leetcode.com/problems/linked-list-random-node/

------------------------------------------------------------------------

# Must Know For FAANG

Graph - Dijkstra - Bellman Ford - Kruskal - Prim - Tarjan - Kahn

Strings - KMP - Rabin Karp - Manacher

Dynamic Programming - Kadane

Math - Euclid GCD - Sieve of Eratosthenes

Bit - Brian Kernighan
