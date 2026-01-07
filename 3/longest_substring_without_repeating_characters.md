# 3. Longest Substring Without Repeating Characters

**Difficulty:** Medium

## Problem Description

Given a string `s`, find the length of the **longest substring** without repeating characters.

A **substring** is a contiguous sequence of characters within a string.

## Examples

**Example 1:**
- **Input:** `s = "abcabcbb"`
- **Output:** `3`
- **Explanation:** The answer is "abc", with the length of 3.

**Example 2:**
- **Input:** `s = "bbbbb"`
- **Output:** `1`
- **Explanation:** The answer is "b", with the length of 1.

**Example 3:**
- **Input:** `s = "pwwkew"`
- **Output:** `3`
- **Explanation:** The answer is "wke", with the length of 3. Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

## Constraints:
- `0 <= s.length <= 5 * 10^4`
- `s` consists of English letters, digits, symbols and spaces.

---

## 1. Sliding Window (Set)

We use a sliding window approach with a hash set to keep track of the unique characters in the current window. If we encounter a character that is already in the set, we shrink the window from the left until the duplicate is removed.

```python
def lengthOfLongestSubstring(s):
    char_set = set()
    l = 0
    res = 0
    
    for r in range(len(s)):
        while s[r] in char_set:
            char_set.remove(s[l])
            l += 1
        char_set.add(s[r])
        res = max(res, r - l + 1)
        
    return res
```

**Complexity:**
- **Time:** $O(n)$ where $n$ is the length of the string. Each character is visited at most twice.
- **Space:** $O(\min(m, n))$ where $m$ is the size of the character set (e.g., 256 for ASCII).

---

## 2. Optimized Sliding Window (Map)

Instead of shrinking the window one by one, we can store the **last index** of each character in a hash map. If we find a duplicate, we can jump the `left` pointer directly to the index after the last occurrence of that character.

```python
def lengthOfLongestSubstring(s):
    char_map = {} # char : last index
    l = 0
    res = 0
    
    for r in range(len(s)):
        if s[r] in char_map:
            # jump l to the right of the previous occurrence
            # but only if it's within the current window
            l = max(l, char_map[s[r]] + 1)
            
        char_map[s[r]] = r
        res = max(res, r - l + 1)
        
    return res
```

**Complexity:**
- **Time:** $O(n)$ - one pass through the string.
- **Space:** $O(\min(m, n))$ where $m$ is the size of the character set.

---

## Comparison Table

| Approach | Time Complexity | Space Complexity | Notes |
| :--- | :--- | :--- | :--- |
| **Sliding Window (Set)** | $O(n)$ | $O(\min(m, n))$ | Simple sliding window. |
| **Sliding Window (Map)** | $O(n)$ | $O(\min(m, n))$ | Optimized with jumps. |
