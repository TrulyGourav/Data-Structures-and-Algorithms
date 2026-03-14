# FAANG Bit Manipulation -- Quick Revision Notes

Concise high‑signal notes for interview preparation (FAANG / product
companies).\
Focus: **patterns, formulas, observations, and reusable tricks.**

------------------------------------------------------------------------

# 1. Binary Basics

**Bit Positions** - LSB → bit 0 - MSB → highest bit

**Power Representation** n = Σ (bit_i \* 2\^i)

Example\
13 = 1101 = 8 + 4 + 1

------------------------------------------------------------------------

# 2. Most Important Bit Operations

**Set a bit** n \| (1 \<\< i)

**Clear a bit** n & \~(1 \<\< i)

**Toggle a bit** n \^ (1 \<\< i)

**Check if bit is set** (n \>\> i) & 1

------------------------------------------------------------------------

# 3. Identity Laws

a \^ a = 0\
a \^ 0 = a\
a & 0 = 0\
a \| 0 = a\
a & a = a

Special:

a \^ b \^ a = b

Duplicates cancel using XOR.

Used in: - Single Number - Missing Number - XOR pair problems

------------------------------------------------------------------------

# 4. XOR Properties

Commutative\
a \^ b = b \^ a

Associative\
(a \^ b) \^ c = a \^ (b \^ c)

Order of XOR operations does not matter.

------------------------------------------------------------------------

# 5. Remove Last Set Bit

n & (n - 1)

Example

n = 12 (1100)\
n-1 = 11 (1011)

Result = 1000

Removes the **rightmost set bit**.

Used in: - Counting set bits - Power of two check

------------------------------------------------------------------------

# 6. Check Power of Two

n & (n-1) == 0

Example

8 = 1000\
7 = 0111

1000 & 0111 = 0

------------------------------------------------------------------------

# 7. Extract Rightmost Set Bit

n & (-n)

Example

n = 12 = 1100\
Result = 0100

Isolates the **lowest set bit**.

Used in: - Two unique numbers problem - Bit partitioning

------------------------------------------------------------------------

# 8. Count Set Bits Efficiently

Brian Kernighan Algorithm

while(n \> 0): n = n & (n-1) count++

Time Complexity\
O(number_of_set_bits)

------------------------------------------------------------------------

# 9. XOR Range Pattern

XOR from 1 to n follows pattern:

n % 4 == 0 → n\
n % 4 == 1 → 1\
n % 4 == 2 → n + 1\
n % 4 == 3 → 0

Used in: - Range XOR problems - Missing number problems

------------------------------------------------------------------------

# 10. Swap Without Temp

a = a \^ b\
b = a \^ b\
a = a \^ b

------------------------------------------------------------------------

# 11. Subset Generation (Bitmask)

For array size n

total subsets = 2\^n

Loop

for mask in 0 → (1 \<\< n)

Check element presence

if(mask & (1 \<\< i))

Used in: - Subset generation - Bitmask DP - Backtracking optimization

------------------------------------------------------------------------

# 12. Bit Counting Pattern (Extremely Important)

If numbers repeat **k times except one**.

Count bits **column-wise**.

unique_bit_i = (sum_of_bits_i % k)

Example

nums = \[2,2,2,5\]

2 = 010\
2 = 010\
2 = 010\
5 = 101

Column counts

1 3 1

Mod 3

1 0 1

Result = 101 = 5

General rule

unique_bit_i = (sum_of_bits_i % k)

Works for:

Single number II\
Any "repeat k times except one" problem

------------------------------------------------------------------------

# 13. Two Unique Numbers Trick

If two numbers appear once:

xor_all = a \^ b

Find differentiating bit

diff = xor_all & (-xor_all)

Split numbers into two groups using this bit.

------------------------------------------------------------------------

# 14. Common Bit Masks

All bits up to n:

(1 \<\< n) - 1

Example

(1 \<\< 4) - 1 = 1111

------------------------------------------------------------------------

# 15. Fast Multiply / Divide

Multiply by power of 2

n \<\< k

Divide by power of 2

n \>\> k

------------------------------------------------------------------------

# 16. Check Even / Odd

n & 1

1 → odd\
0 → even

------------------------------------------------------------------------

# 17. Pattern Recognition Guide

Pattern 1 --- XOR cancellation

Used when duplicates appear **even number of times**.

Examples: - Single Number - Missing Number

Pattern 2 --- Bit counting

Used when numbers repeat **k times**.

Logic:

bit_sum % k

Pattern 3 --- Isolate distinguishing bit

Used when **two numbers are unique**.

Technique:

xor & (-xor)

Pattern 4 --- Subset enumeration

Used when

n \<= 20

Use bitmask enumeration.

------------------------------------------------------------------------

# 18. Common FAANG Problem Types

XOR cancellation → Single Number\
Bit counting → Single Number II\
Rightmost bit trick → Two unique numbers\
Power-of-two property → Bit property problems\
Subset masks → Subsets / bitmask DP\
Range XOR → Missing number

------------------------------------------------------------------------

# 19. Golden Interview Heuristics

If problem says:

All numbers appear twice except one → XOR

All numbers appear k times except one → Bit counting % k

Two numbers appear once → XOR + split using rightmost set bit

------------------------------------------------------------------------

# 20. Mental Model

Always think **bit column-wise**, not number-wise.

Every number contributes to columns:

bit0\
bit1\
bit2\
bit3

Many interview problems exploit this idea.

------------------------------------------------------------------------

# ⭐ Five Core Tricks To Memorize

n & (n-1)\
n & (-n)\
XOR cancellation\
Bit counting % k\
Subset mask (1 \<\< n)

These tricks solve **a large percentage of bit manipulation interview
problems**.
