# 49. Group Anagrams

**Difficulty:** Medium

## Problem Description

Given an array of strings `strs`, group the **anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Examples

**Example 1:**
- **Input:** `strs = ["eat","tea","tan","ate","nat","bat"]`
- **Output:** `[["bat"],["nat","tan"],["ate","eat","tea"]]`

**Example 2:**
- **Input:** `strs = [""]`
- **Output:** `[[""]]`

**Example 3:**
- **Input:** `strs = ["a"]`
- **Output:** `[["a"]]`

## Constraints:
- `1 <= strs.length <= 10^4`
- `0 <= strs[i].length <= 100`
- `strs[i]` consists of lowercase English letters.

---

## 1. Sorting Approach

Since all anagrams results in the same string when sorted, we can use the sorted string as a key in a hash map.

```python
from collections import defaultdict

def groupAnagrams(strs):
    anagram_map = defaultdict(list)
    
    for s in strs:
        # Sort the string and use it as a key
        sorted_s = "".join(sorted(s))
        anagram_map[sorted_s].append(s)
        
    return list(anagram_map.values())
```

**Complexity:**
- **Time:** $O(m \cdot n \log n)$, where $m$ is the number of strings and $n$ is the maximum length of a string.
- **Space:** $O(m \cdot n)$ to store the groups.

---

## 2. Character Count Approach (Optimal)

Instead of sorting, we can use the count of each character (a-z) as a key. This avoids the $O(n \log n)$ sorting cost.

```python
from collections import defaultdict

def groupAnagrams(strs):
    res = defaultdict(list)
    
    for s in strs:
        count = [0] * 26 # a-z
        for char in s:
            count[ord(char) - ord('a')] += 1
            
        # Convert list to tuple so it can be used as a key
        res[tuple(count)].append(s)
        
    return list(res.values())
```

**Complexity:**
- **Time:** $O(m \cdot n)$ where $m$ is the number of strings and $n$ is the maximum length of a string.
- **Space:** $O(m \cdot 26)$ for the keys in the hash map.

---

## 3. Comparison

| Approach | Time Complexity | Space Complexity |
| :--- | :--- | :--- |
| **Sorting** | $O(m \cdot n \log n)$ | $O(m \cdot n)$ |
| **Char Count** | $O(m \cdot n)$ | $O(m \cdot n)$ |
