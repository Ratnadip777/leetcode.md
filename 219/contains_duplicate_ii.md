# 219. Contains Duplicate II

**Difficulty:** Easy

## Problem Description

Given an integer array `nums` and an integer `k`, return `true` if there exist two distinct indices `i` and `j` in the array such that `nums[i] == nums[j]` and `abs(i - j) <= k`.

## Examples

**Example 1:**
- **Input:** `nums = [1,2,3,1]`, `k = 3`
- **Output:** `true`

**Example 2:**
- **Input:** `nums = [1,0,1,1]`, `k = 1`
- **Output:** `true`

**Example 3:**
- **Input:** `nums = [1,2,3,1,2,3]`, `k = 2`
- **Output:** `false`

---

## 1. Brute Force Approach

Check every pair of elements `(i, j)` and see if they are equal and their distance is within `k`.

```python
def containsNearbyDuplicate(nums, k):
    n = len(nums)
    for i in range(n):
        for j in range(i + 1, min(i + k + 1, n)):
            if nums[i] == nums[j]:
                return True
    return False
```

**Complexity:**
- **Time:** $O(n \times k)$
- **Space:** $O(1)$

---

## 2. Hash Map Approach (Optimal)

Maintain a hash map that stores the most recent index of each element. As we iterate through the array, if we find an element that is already in the map, we check if the difference between the current index and the stored index is $\le k$.

```python
def containsNearbyDuplicate(nums, k):
    index_map = {}  # val : last_seen_index
    for i, n in enumerate(nums):
        if n in index_map and i - index_map[n] <= k:
            return True
        index_map[n] = i
    return False
```

**Complexity:**
- **Time:** $O(n)$
- **Space:** $O(n)$

---

## 3. Sliding Window Approach (Hash Set)

Maintain a sliding window of size `k` using a hash set. If the set already contains the current number, return `true`. If the window exceeds size `k`, remove the oldest element.

```python
def containsNearbyDuplicate(nums, k):
    window = set()
    for i in range(len(nums)):
        if i > k:
            window.remove(nums[i - k - 1])
        if nums[i] in window:
            return True
        window.add(nums[i])
    return False
```

**Complexity:**
- **Time:** $O(n)$
- **Space:** $O(k)$
