# 167. Two Sum II - Input Array Is Sorted

**Difficulty:** Medium

## Problem Description

Given a **1-indexed** array of integers `numbers` that is already **sorted in non-decreasing order**, find two numbers such that they add up to a specific `target` number. Let these two numbers be `numbers[index1]` and `numbers[index2]` where `1 <= index1 < index2 <= numbers.length`.

Return the indices of the two numbers, `index1` and `index2`, **added by one** as an integer array `[index1, index2]` of length 2.

The tests are generated such that there is **exactly one solution**. You **may not** use the same element twice.

Your solution must use only constant extra space.

## Examples

**Example 1:**
- **Input:** `numbers = [2,7,11,15]`, `target = 9`
- **Output:** `[1,2]`
- **Explanation:** The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].

**Example 2:**
- **Input:** `numbers = [2,3,4]`, `target = 6`
- **Output:** `[1,3]`
- **Explanation:** The sum of 2 and 4 is 6. Therefore index1 = 1, index2 = 3. We return [1, 3].

**Example 3:**
- **Input:** `numbers = [-1,0]`, `target = -1`
- **Output:** `[1,2]`
- **Explanation:** The sum of -1 and 0 is -1. Therefore index1 = 1, index2 = 2. We return [1, 2].

## Constraints:
- $2 \le \text{numbers.length} \le 3 \times 10^4$
- $-1000 \le \text{numbers[i]} \le 1000$
- `numbers` is sorted in **non-decreasing order**.
- $-1000 \le \text{target} \le 1000$
- The tests are generated such that there is **exactly one solution**.

---

## 1. Two-Pointer Approach (Optimal)

Since the array is already sorted, we can use two pointers: one at the beginning (`left`) and one at the end (`right`). 
- If the current sum is too small, we increment the `left` pointer to get a larger sum.
- If the current sum is too large, we decrement the `right` pointer to get a smaller sum.

```python
def twoSum(numbers, target):
    l, r = 0, len(numbers) - 1
    
    while l < r:
        curr_sum = numbers[l] + numbers[r]
        
        if curr_sum > target:
            r -= 1
        elif curr_sum < target:
            l += 1
        else:
            return [l + 1, r + 1]
```

**Complexity:**
- **Time:** $O(n)$ where $n$ is the length of the array.
- **Space:** $O(1)$.

---

## 2. Binary Search Approach (Alternative)

For each element `numbers[i]`, we can binary search for the complement `target - numbers[i]` in the remaining part of the array `numbers[i+1:]`.

```python
def twoSum(numbers, target):
    for i in range(len(numbers)):
        low, high = i + 1, len(numbers) - 1
        complement = target - numbers[i]
        
        while low <= high:
            mid = low + (high - low) // 2
            if numbers[mid] == complement:
                return [i + 1, mid + 1]
            elif numbers[mid] < complement:
                low = mid + 1
            else:
                high = mid - 1
```

**Complexity:**
- **Time:** $O(n \log n)$.
- **Space:** $O(1)$.

---

## Comparison Table

| Approach | Time Complexity | Space Complexity | Notes |
| :--- | :--- | :--- | :--- |
| **Two Pointers** | $O(n)$ | $O(1)$ | Most efficient for sorted arrays. |
| **Binary Search** | $O(n \log n)$ | $O(1)$ | Useful if the search space is large. |
