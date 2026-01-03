# 217. Contains Duplicate

**Difficulty:** Easy

## Problem Description

Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

## Examples

**Example 1:**
- **Input:** `nums = [1,2,3,1]`
- **Output:** `true`
- **Explanation:** The element 1 occurs at the indices 0 and 3.

**Example 2:**
- **Input:** `nums = [1,2,3,4]`
- **Output:** `false`
- **Explanation:** All elements are distinct.

**Example 3:**
- **Input:** `nums = [1,1,1,3,3,4,3,2,4,2]`
- **Output:** `true`

---

## 1. Brute Force Approach

Compare every pair of elements to see if any two are equal.

```python
def containsDuplicate(nums):
    for i in range(len(nums)):
        for j in range(i + 1, len(nums)):
            if nums[i] == nums[j]:
                return True
    return False
```

**Complexity:**
- **Time:** $O(n^2)$
- **Space:** $O(1)$

---

## 2. Sorting Approach

Sort the array first. If there are any duplicates, they will be adjacent in the sorted array.

```python
def containsDuplicate(nums):
    nums.sort()
    for i in range(len(nums) - 1):
        if nums[i] == nums[i + 1]:
            return True
    return False
```

**Complexity:**
- **Time:** $O(n \log n)$
- **Space:** $O(1)$ or $O(n)$ depending on the sorting algorithm.

---

## 3. Hash Set Approach (Optimal)

Use a hash set to store the elements we have seen so far. For each element, check if it's already in the set.

```python
def containsDuplicate(nums):
    seen = set()
    for n in nums:
        if n in seen:
            return True
        seen.add(n)
    return False
```

**Complexity:**
- **Time:** $O(n)$ because set lookups and insertions are $O(1)$ on average.
- **Space:** $O(n)$ to store elements in the set.
