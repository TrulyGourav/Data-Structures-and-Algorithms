# 204. Count Primes

🔗 **LeetCode Problem:** https://leetcode.com/problems/count-primes/

------------------------------------------------------------------------

# 🧩 Problem Statement

Given an integer `n`, return **the number of prime numbers that are
strictly less than `n`**.

A **prime number** is a natural number greater than `1` that has
**exactly two divisors: 1 and itself**.

### Example

    Input: n = 10
    Output: 4

    Explanation:
    Prime numbers less than 10 are:
    2, 3, 5, 7

------------------------------------------------------------------------

# 🧠 Core Intuition (MOST IMPORTANT)

Instead of **checking every number individually for primality**, we use
a smarter observation:

👉 **If a number is prime, all of its multiples cannot be prime.**

Example:

    2 is prime → eliminate 4,6,8,10...
    3 is prime → eliminate 6,9,12...
    5 is prime → eliminate 10,15...

So the strategy becomes:

1.  Assume **all numbers are prime initially**
2.  Start from the **smallest prime (2)**
3.  **Mark all multiples as non-prime**
4.  Move forward and repeat

This algorithm is known as:

# ⚡ Sieve of Eratosthenes

A famous algorithm that **filters primes instead of testing them
individually**.

------------------------------------------------------------------------

# 🔍 Conceptual Understanding

We maintain a **boolean array**:

    index  → number
    value  → isPrime?

Example for `n = 10`

Initial state:

    Number:   0 1 2 3 4 5 6 7 8 9 10
    isPrime:  T T T T T T T T T T  T

Step 1 --- Prime = 2

    Mark multiples of 2

    4,6,8,10 → false

    Number:   0 1 2 3 4 5 6 7 8 9 10
    isPrime:  T T T T F T F T F T  F

Step 2 --- Prime = 3

    Mark multiples of 3

    6,9 → false

    Number:   0 1 2 3 4 5 6 7 8 9 10
    isPrime:  T T T T F T F T F F  F

Remaining primes:

    2,3,5,7

Count = **4**

------------------------------------------------------------------------

# ⏱️ Time & Space Complexity

  Complexity   Value
  ------------ --------------------
  Time         **O(n log log n)**
  Space        **O(n)**

Why `log log n`?

Because the number of marking operations decreases rapidly as primes
grow larger.

------------------------------------------------------------------------

# 🌳 Visualization of the Sieve Process

Example `n = 12`

    Start
    │
    ├── Prime = 2
    │      Mark → 4,6,8,10,12
    │
    ├── Prime = 3
    │      Mark → 6,9,12
    │
    ├── Prime = 4 (skipped because already marked)
    │
    ├── Prime = 5
    │      Mark → 10
    │
    └── Prime = 7
           Mark → none within range

Final primes:

    2,3,5,7,11

------------------------------------------------------------------------

# 💻 Java Implementation

``` java
class Solution {
    public int countPrimes(int n) {

        boolean[] arr = new boolean[n + 1];
        int ans = 0;

        Arrays.fill(arr, true);

        for(int i = 2; i < n; i++){   // 0 and 1 are not prime

            if(arr[i]){

                ans++;

                int j = 2 * i;

                while(j <= n){
                    arr[j] = false;
                    j += i;
                }
            }
        }

        return ans;
    }
}
```

------------------------------------------------------------------------

# 🔁 Other Possible Approaches

  -----------------------------------------------------------------------
  Approach              Idea             Complexity
  --------------------- ---------------- --------------------------------
  Brute Force           Check every      O(n√n)
                        number for       
                        primality by     
                        dividing up to   
                        √n               

  Improved Prime Check  Check            O(n√n)
                        divisibility up  
                        to √n for each   
                        number           

  Sieve of Eratosthenes Eliminate        **O(n log log n)** ✅ (Current
                        multiples of     Solution)
                        primes           

  Optimized Sieve       Start marking    O(n log log n)
                        from `i*i`       
                        instead of `2*i` 

  Segmented Sieve       Used when `n` is O(n log log n)
                        extremely large  
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 🔗 Related Problems (Pattern Recognition)

These problems use **Sieve / Prime logic**.

### LeetCode

• https://leetcode.com/problems/count-primes/\
• https://leetcode.com/problems/prime-arrangements/\
• https://leetcode.com/problems/closest-prime-numbers-in-range/\
• https://leetcode.com/problems/count-primes/

### Advanced Prime Problems

• Segmented Sieve\
• Prime Factorization\
• Euler Totient Function

------------------------------------------------------------------------

# 🧩 Pattern Recognition

If you see:

    Count primes
    Find primes in range
    Mark multiples
    Prime factors

Your brain should instantly think:

# 👉 SIEVE OF ERATOSTHENES

------------------------------------------------------------------------

# 🧠 Interview Memory Trick (Never Forget This)

Imagine **numbers sitting in a classroom**:

    2,3,4,5,6,7,8,9,10...

Now **2 stands up and says:**

> "Everyone who is my multiple, leave the class!"

So:

    4,6,8,10 leave

Then **3 stands up:**

> "My multiples also leave!"

    6,9 leave

The students left sitting are:

    2,3,5,7

Those are the **real primes**.

💡 **Key memory trigger:**

    Prime discovered → eliminate its multiples

This mental image makes the algorithm **impossible to forget in
interviews.**

------------------------------------------------------------------------

⭐ **Pro Tip for Interviews**

Always mention:

> "This problem can be solved using the Sieve of Eratosthenes which
> efficiently eliminates multiples of primes."

Interviewers love hearing this.

------------------------------------------------------------------------
