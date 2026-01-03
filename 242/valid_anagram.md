# 242. Valid Anagram

**Difficulty:** Easy

## Problem Description

Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Examples

**Example 1:**
- **Input:** `s = "anagram"`, `t = "nagaram"`
- **Output:** `true`

**Example 2:**
- **Input:** `s = "rat"`, `t = "car"`
- **Output:** `false`

## Constraints:
- `1 <= s.length, t.length <= 5 * 10^4`
- `s` and `t` consist of lowercase English letters.

---

## 1. Sorting Approach

If two strings are anagrams, sorting them will result in the same string.

```python
def isAnagram(s, t):
    return sorted(s) == sorted(t)
```

**Complexity:**
- **Time:** $O(n \log n)$ due to sorting.
- **Space:** $O(n)$ or $O(1)$ depending on the language/sorting implementation.

---

## 2. Hash Map Approach (Frequency Count)

Count the frequency of each character in both strings. If the frequencies match, the strings are anagrams.

```python
def isAnagram(s, t):
    if len(s) != len(t):
        return False
    
    countS, countT = {}, {}
    
    for i in range(len(s)):
        countS[s[i]] = 1 + countS.get(s[i], 0)
        countT[t[i]] = 1 + countT.get(t[i], 0)
    
    return countS == countT
```

**Complexity:**
- **Time:** $O(n)$ where $n$ is the length of the strings.
- **Space:** $O(1)$ because the hash map size is bounded by the number of unique characters (26 for lowercase English letters).

---

## 3. Single Hash Map Approach (Optimal Space)

Use a single hash map to increment counts for `s` and decrement for `t`. If all counts in the map are zero at the end, they are anagrams.

```python
from collections import Counter

def isAnagram(s, t):
    return Counter(s) == Counter(t)
```

Alternatively, without `Counter`:

```python
def isAnagram(s, t):
    if len(s) != len(t):
        return False
        
    count = {}
    for char in s:
        count[char] = count.get(char, 0) + 1
        
    for char in t:
        if char not in count or count[char] == 0:
            return False
        count[char] -= 1
        
    return True
```

**Complexity:**
- **Time:** $O(n)$
- **Space:** $O(1)$ (max 26 characters).
