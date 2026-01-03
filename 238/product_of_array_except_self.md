# 238. Product of Array Except Self

**Difficulty:** Medium

## Problem Description

Given an integer array `nums`, return an array `answer` such that `answer[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

The product of any prefix or suffix of `nums` is guaranteed to fit in a **32-bit** integer.

You must write an algorithm that runs in $O(n)$ time and without using the division operation.

## Examples

**Example 1:**
- **Input:** `nums = [1,2,3,4]`
- **Output:** `[24,12,8,6]`

**Example 2:**
- **Input:** `nums = [-1,1,0,-3,3]`
- **Output:** `[0,0,9,0,0]`

## Constraints:
- `2 <= nums.length <= 10^5`
- `-30 <= nums[i] <= 30`
- The product of any prefix or suffix of `nums` is guaranteed to fit in a **32-bit** integer.

---

## 1. Prefix and Suffix Arrays Approach

We can use two arrays to store the prefix products and suffix products of each element. The result for `nums[i]` will be `prefix[i] * suffix[i]`.

```python
def productExceptSelf(nums):
    n = len(nums)
    prefix = [1] * n
    suffix = [1] * n
    
    # Calculate prefix products
    for i in range(1, n):
        prefix[i] = prefix[i-1] * nums[i-1]
        
    # Calculate suffix products
    for i in range(n-2, -1, -1):
        suffix[i] = suffix[i+1] * nums[i+1]
        
    return [prefix[i] * suffix[i] for i in range(n)]
```

**Complexity:**
- **Time:** $O(n)$ where $n$ is the length of the array.
- **Space:** $O(n)$ for the prefix and suffix arrays.

---

## 2. Optimized Space Approach (One Array)

We can optimize the space by using the result array itself to store prefix products first, and then multiplying it by suffix products on the fly.

```python
def productExceptSelf(nums):
    n = len(nums)
    res = [1] * n
    
    # Prefix pass
    prefix = 1
    for i in range(n):
        res[i] = prefix
        prefix *= nums[i]
        
    # Suffix pass
    suffix = 1
    for i in range(n-1, -1, -1):
        res[i] *= suffix
        suffix *= nums[i]
        
    return res
```

**Complexity:**
- **Time:** $O(n)$
- **Space:** $O(1)$ (Note: The output array does not count as extra space for the purpose of complexity analysis).

---

## Summary Comparison

| Approach | Time Complexity | Space Complexity | Notes |
| :--- | :--- | :--- | :--- |
| **Prefix/Suffix Arrays** | $O(n)$ | $O(n)$ | Easier to understand. |
| **Optimized Space** | $O(n)$ | $O(1)$ | Most efficient. |
