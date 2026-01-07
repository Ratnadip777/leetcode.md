# 643. Maximum Average Subarray I

**Difficulty:** Easy

## Problem Description

You are given an integer array `nums` consisting of `n` elements, and an integer `k`.

Find a contiguous subarray whose **length is equal to `k`** that has the maximum average value and return this value. Any answer with a calculation error less than $10^{-5}$ will be accepted.

## Examples

**Example 1:**
- **Input:** `nums = [1,12,-5,-6,50,3]`, `k = 4`
- **Output:** `12.75000`
- **Explanation:** Maximum average is $(12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75$.

**Example 2:**
- **Input:** `nums = [5]`, `k = 1`
- **Output:** `5.00000`

## Constraints:
- $n = \text{nums.length}$
- $1 \le k \le n \le 10^5$
- $-10^4 \le \text{nums[i]} \le 10^4$

---

## 1. Sliding Window Approach (Optimal)

Instead of recalculating the sum of every subarray of length `k`, we can use a sliding window. We start with the sum of the first `k` elements, then slide the window by adding the next element and removing the first element of the previous window.

```python
def findMaxAverage(nums, k):
    # Initialize the sum of the first window
    curr_sum = sum(nums[:k])
    max_sum = curr_sum
    
    # Slide the window across the array
    for i in range(k, len(nums)):
        # Add the next element and remove the leftmost element
        curr_sum += nums[i] - nums[i - k]
        max_sum = max(max_sum, curr_sum)
        
    return max_sum / k
```

**Complexity:**
- **Time:** $O(n)$ where $n$ is the length of the array. We travel through the array once.
- **Space:** $O(1)$ as we only store a few variables for the sums.

---

## 2. Brute Force Approach (Time Limit Exceeded)

Check every possible contiguous subarray of length `k`.

```python
def findMaxAverage(nums, k):
    max_avg = -float('inf')
    for i in range(len(nums) - k + 1):
        curr_sum = 0
        for j in range(i, i + k):
            curr_sum += nums[j]
        max_avg = max(max_avg, curr_sum / k)
    return max_avg
```

**Complexity:**
- **Time:** $O(n \times k)$
- **Space:** $O(1)$

---

## Comparison Table

| Approach | Time Complexity | Space Complexity | Notes |
| :--- | :--- | :--- | :--- |
| **Sliding Window** | $O(n)$ | $O(1)$ | Efficient and recommended. |
| **Brute Force** | $O(n \times k)$ | $O(1)$ | TLE for large inputs. |
