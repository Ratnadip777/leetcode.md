# 1. Two Sum

**Difficulty:** Easy

## Problem Description

Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

## Examples

**Example 1:**
- **Input:** `nums = [2,7,11,15]`, `target = 9`
- **Output:** `[0,1]`

**Example 2:**
- **Input:** `nums = [3,2,4]`, `target = 6`
- **Output:** `[1,2]`

---

## 1. Brute Force Approach

Check every pair of numbers using nested loops.

```python
def twoSum(nums, target):
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            if nums[i] + nums[j] == target:
                return [i, j]
```

**Complexity:**
- **Time:** $O(n^2)$
- **Space:** $O(1)$

---

## 2. Binary Search Approach

This approach requires sorting the array first. Note that since we need to return original indices, we must store them before sorting.

1. Store numbers with their original indices and sort them.
2. Iterate through each number `nums[i]`.
3. Binary Search for the complement (`target - nums[i]`) in the remaining part of the sorted array.

```python
def twoSum(nums, target):
    # Store value with index and sort
    sorted_nums = sorted((val, i) for i, val in enumerate(nums))
    
    for i in range(len(sorted_nums)):
        complement = target - sorted_nums[i][0]
        # Binary search for complement
        low, high = i + 1, len(sorted_nums) - 1
        while low <= high:
            mid = (low + high) // 2
            if sorted_nums[mid][0] == complement:
                return [sorted_nums[i][1], sorted_nums[mid][1]]
            elif sorted_nums[mid][0] < complement:
                low = mid + 1
            else:
                high = mid - 1
```

**Complexity:**
- **Time:** $O(n \log n)$ due to sorting and $n$ binary searches.
- **Space:** $O(n)$ to store the original indices.

---

## 3. Hash Map Approach (One-Pass)

This is the most efficient approach. We use a hash map to store numbers we have seen so far and their indices.

1. Iterate through the array.
2. Calculate the complement needed to reach the target (`diff = target - nums[i]`).
3. If the complement exists in our map, return the current index and the index of the complement.
4. If not, add the current number and its index to the map.

```python
def twoSum(nums, target):
    prev_map = {}  # val : index

    for i, n in enumerate(nums):
        diff = target - n
        if diff in prev_map:
            return [prev_map[diff], i]
        prev_map[n] = i
```

**Complexity:**
- **Time:** $O(n)$ as we only traverse the list once and hash map lookups are $O(1)$.
- **Space:** $O(n)$ to store elements in the hash map.
