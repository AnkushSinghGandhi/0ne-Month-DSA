# 🧠 Sliding Window Technique
Concept:
Sliding Window is a technique for reducing nested loops to linear time when we need to examine subsets of a sequence.
Instead of re-evaluating every subarray or substring from scratch, we "slide" a window across the input, adding the next element and removing the previous.

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

---

## Common Patterns

---

### 🔹 1. Fixed Window Size – Maximum/Minimum Sum or Average

**🧠 Problem Pattern**:
"Find the max/min sum (or average) of any subarray of size `k`."

**Example**:
Find max sum of subarray of size `k = 3`
Array: `[2, 1, 5, 1, 3, 2]`

```text
Initial Window:        [2  1  5]  -> sum = 8
Slide Right:              [1  5  1]  -> sum = 7
Slide Right:                 [5  1  3]  -> sum = 9 (max)
Slide Right:                    [1  3  2]  -> sum = 6
```

✅ Final Answer: `9`

---

### 🔹 2. Variable Window Size – Longest Substring with Condition

**🧠 Problem Pattern**:
"Find the longest subarray/substring where a condition holds (like unique characters or sum < target)."

**Example**:
Longest substring without repeating characters
String: `"abcabcbb"`

```text
Window: [a]     ✔ Unique
Window: [a b]   ✔ Unique
Window: [a b c] ✔ Unique
Window: [a b c a] ❌ a repeated → shrink from left
Shrink to: [b c a] ✔

Continue...
```

✅ Final Answer: Length `3` (`"abc"`)

---

### 🔹 3. Shrinking Window – Minimum Size Subarray with a Target

**🧠 Problem Pattern**:
"Find the smallest window/subarray whose **sum ≥ target**."

**Example**:
Array = `[2,3,1,2,4,3]`, Target = `7`

```text
Expand window:
[2] → sum = 2
[2,3] → sum = 5
[2,3,1] → sum = 6
[2,3,1,2] → sum = 8 ✔

Now start shrinking:
[3,1,2] → sum = 6 ❌
[1,2,4] → sum = 7 ✔ window size = 3
[2,4] → sum = 6 ❌
[4,3] → sum = 7 ✔ window size = 2 ✅
```

✅ Final Answer: `2`

---

### 🔹 4. Sliding Window with Hashmap – Anagrams or Frequency Checks

**🧠 Problem Pattern**:
"Find substrings that are anagrams / permutations of a pattern."

**Example**:
Find all anagrams of `"ab"` in `"cbaebabacd"`

```text
Pattern count: a:1, b:1
Sliding over string:

[c b] → match ✔ at index 0
[b a] → match ✔ at index 1
[a e] → ❌
[e b] → ❌
...

Each time: update window count, compare to pattern count
```

✅ Final Output: `[0, 6]`

---

### 🔹 5. Max in Every Window of Size K (Deque-based)

**🧠 Problem Pattern**:
"Return an array of max values for each window of size `k`."

Use a **deque** to store indices of potential max elements.

Example: `nums = [1,3,-1,-3,5,3,6,7], k = 3`

```text
First window: [1, 3, -1] → max = 3
Next window: [3, -1, -3] → max = 3
Next window: [-1, -3, 5] → max = 5
...

Maintain deque of decreasing values (monotonic)
```

✅ Output: `[3,3,5,5,6,7]`

---

## 🧩 Summary Table of Patterns

| Pattern Type       | Window Size | Use Case                                 |
| ------------------ | ----------- | ---------------------------------------- |
| Fixed Size         | Fixed       | Max sum, average, count, vowels, etc.    |
| Variable Size      | Dynamic     | Longest/shortest subarray with condition |
| Shrinking Window   | Dynamic     | Minimum size with target                 |
| Hashmap/Set Window | Varies      | Frequency, anagrams, permutations        |
| Monotonic Deque    | Fixed       | Max/Min in each window                   |



