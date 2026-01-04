# 357. Count Numbers with Unique Digits

**Difficulty:** Medium

## Problem Description

Given an integer `n`, return the count of all numbers with unique digits, `x`, where $0 \le x < 10^n$.

## Examples

**Example 1:**
- **Input:** `n = 2`
- **Output:** `91`
- **Explanation:** The answer should be the total numbers in the range of $0 \le x < 100$, excluding `11, 22, 33, 44, 55, 66, 77, 88, 99`.

**Example 2:**
- **Input:** `n = 0`
- **Output:** `1`

## Constraints:
- `0 <= n <= 8`

---

## 1. Combinatorial Approach

This is a permutations problem. 

- For $n=0$: Only one number (0). Result = 1.
- For $n=1$: Numbers 0-9. Result = 10.
- For $n \ge 2$:
    - The first digit can be any of 9 digits (1-9).
    - The second digit can be any of 9 digits (0-9, excluding the first digit).
    - The third digit can be any of 8 digits (excluding the first two).
    - ... and so on.

```python
def countNumbersWithUniqueDigits(n):
    if n == 0:
        return 1
    
    res = 10
    unique_digits = 9
    available_choices = 9
    
    while n > 1 and available_choices > 0:
        unique_digits *= available_choices
        res += unique_digits
        available_choices -= 1
        n -= 1
        
    return res
```

**Complexity:**
- **Time:** $O(n)$ where $n \le 10$. Since $n$ is small, this is effectively $O(1)$.
- **Space:** $O(1)$.

---

## 2. Dynamic Programming Approach

We can think of this as $f(n) = f(n-1) + \text{count of unique digit numbers with exactly } n \text{ digits}$.

```python
def countNumbersWithUniqueDigits(n):
    if n == 0: return 1
    if n == 1: return 10
    
    dp = [0] * (n + 1)
    dp[0] = 1
    dp[1] = 10
    
    # number of unique digits for exactly i digits
    # for i=2: 9 * 9
    # for i=3: 9 * 9 * 8
    curr_unique = 81
    for i in range(2, n + 1):
        dp[i] = dp[i-1] + curr_unique
        curr_unique *= (10 - i)
        
    return dp[n]
```

**Complexity:**
- **Time:** $O(n)$
- **Space:** $O(n)$ (can be optimized to $O(1)$)

---

## Comparison Table

| Approach | Time Complexity | Space Complexity | Notes |
| :--- | :--- | :--- | :--- |
| **Combinatorics** | $O(1)$ | $O(1)$ | Mathematically direct. |
| **DP** | $O(n)$ | $O(n)$ | Useful for building up counts. |
