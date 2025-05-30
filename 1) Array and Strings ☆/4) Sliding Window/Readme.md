# 🧠 Sliding Window Technique

1) subarray problem
2) find min/max within a window

Concept:

Sliding Window is used for:
1) Longest/shortest substring or subarray with a condition.
2) Maximum or minimum in a window.
3) Number of distinct elements in a range.
4) Sum, average, or count of elements in a subarray.

🔧 Template for Sliding Window (Variable Window Size)
```python
left = 0
for right in range(len(s)):
    # Expand the window
    # Shrink from the left if needed
    # Update result if needed
```
---

## Types of Sliding Window

1. Fixed-size Window
Use when the window size is known in advance.

Example: Max sum of k consecutive elements
```python
def max_sum_k(nums, k):
    max_sum = curr_sum = sum(nums[:k])
    for i in range(k, len(nums)):
        curr_sum += nums[i] - nums[i - k]
        max_sum = max(max_sum, curr_sum)
    return max_sum
```
Input: [1, 4, 2, 10, 23, 3, 1, 0, 20], k = 4
Output: 39 (from subarray [10, 23, 3, 1])

2. Variable-size Window
Use when the window size depends on a condition (e.g., sum < target, or no duplicates).

Example: Longest substring without repeating characters
```python
def length_of_longest_substring(s):
    char_index = {}
    left = max_len = 0
    for right in range(len(s)):
        if s[right] in char_index:
            left = max(left, char_index[s[right]] + 1)
        char_index[s[right]] = right
        max_len = max(max_len, right - left + 1)
    return max_len
```
Input: "abcabcbb"
Output: 3 ("abc")


