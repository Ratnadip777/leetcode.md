# 128. Longest Consecutive Sequence

**Difficulty:** Medium

## Problem Description

Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.

You must write an algorithm that runs in $O(n)$ time.

## Examples

**Example 1:**
- **Input:** `nums = [100, 4, 200, 1, 3, 2]`
- **Output:** `4`
- **Explanation:** The longest consecutive elements sequence is `[1, 2, 3, 4]`. Therefore its length is 4.

**Example 2:**
- **Input:** `nums = [0,3,7,2,5,8,4,6,0,1]`
- **Output:** `9`

## Constraints:
- $0 \le \text{nums.length} \le 10^5$
- $-10^9 \le \text{nums[i]} \le 10^9$

---

## 1. Sorting Approach (Sub-optimal)

The simplest way is to sort the array and then iterate through it to find the longest sequence.

```python
def longestConsecutive(nums):
    if not nums:
        return 0
        
    nums.sort()
    
    longest_streak = 1
    current_streak = 1
    
    for i in range(1, len(nums)):
        if nums[i] != nums[i-1]:
            if nums[i] == nums[i-1] + 1:
                current_streak += 1
            else:
                longest_streak = max(longest_streak, current_streak)
                current_streak = 1
                
    return max(longest_streak, current_streak)
```

**Complexity:**
- **Time:** $O(n \log n)$ due to sorting.
- **Space:** $O(1)$ or $O(n)$ depending on the sorting implementation.

---

## 2. Hash Set Approach (Optimal)

To achieve $O(n)$ time, we use a hash set for $O(1)$ lookups. We only start building a sequence if the current number is the **start** of a sequence (i.e., `num - 1` is not in the set).

```python
def longestConsecutive(nums):
    num_set = set(nums)
    longest = 0
    
    for n in nums:
        # check if its the start of a sequence
        if (n - 1) not in num_set:
            length = 0
            while (n + length) in num_set:
                length += 1
            longest = max(length, longest)
            
    return longest
```

**Complexity:**
- **Time:** $O(n)$. Although there is a `while` loop inside a `for` loop, each number is visited at most twice.
- **Space:** $O(n)$ to store the numbers in a set.

---

## Comparison Table

| Approach | Time Complexity | Space Complexity | Notes |
| :--- | :--- | :--- | :--- |
| **Sorting** | $O(n \log n)$ | $O(1)$ | Simple but doesn't meet the $O(n)$ constraint. |
| **Hash Set** | $O(n)$ | $O(n)$ | Optimal and meets the requirements. |
