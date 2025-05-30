# 🧠 Two Pointers
Concept:
The Two Pointer technique is a powerful and versatile approach used in many array and string problems to reduce time complexity, especially when dealing with sorted data, pairs, or subarrays.

Two Pointers is used for:
1) This is a super versatile pattern, often used for:
2) Palindromes
3) Reversing
4) Substrings
5) Comparing characters from both ends

---

## LeetCode 26 — Remove Duplicates from Sorted Array  
⭐ Idea: Slow/fast pointers: i keeps track of unique placement, j scans through array.
⭐ Tip: When nums[i] != nums[j], we found a new unique — overwrite it.

**Problem:** Remove duplicates in-place so each unique element appears once. Return new length.  
**Example:**
```python
Input: nums = [1,1,2]
Output: 2, nums = [1,2]
```
**Solution:**
```python
def removeDuplicates(nums):
    if not nums:
        return 0
    i = 0
    for j in range(1, len(nums)):
        if nums[j] != nums[i]:
            i += 1
            nums[i] = nums[j]
    return i + 1
```
⏱ Time: O(n) | 💾 Space: O(1)

---

## LeetCode 27 — Remove Element  
⭐ Idea: Use a slow pointer i to rewrite non-val elements.
⭐ Tip: It’s like a "filter" — only keep non-val elements.

**Problem:** Remove all instances of `val` in-place and return new length.  
**Example:**
```python
Input: nums = [3,2,2,3], val = 3  
Output: 2, nums = [2,2,_,_]
```
**Solution:**
```python
def removeElement(nums, val):
    i = 0
    for num in nums:
        if num != val:
            nums[i] = num
            i += 1
    return i
```
⏱ Time: O(n) | 💾 Space: O(1)

---

## LeetCode 283 — Move Zeroes  
⭐ Idea: Move non-zero to front using slow pointer i, swap when needed.
⭐ Tip: Think: "shift non-zero to left" — zeros automatically pile to the right.

**Problem:** Move all `0`’s to the end while maintaining relative order of non-zero elements.  
**Example:**
```python
Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
```
**Solution:**
```python
def moveZeroes(nums):
    i = 0
    for j in range(len(nums)):
        if nums[j] != 0:
            nums[i], nums[j] = nums[j], nums[i]
            i += 1
```
⏱ Time: O(n) | 💾 Space: O(1)

---

## LeetCode 344 — Reverse String  
⭐ Idea: Use two pointers from both ends and swap.
⭐ Tip: Classic reversal — shrink window from both ends.

**Problem:** Reverse an array of characters in-place.  
**Example:**
```python
Input: ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```
**Solution:**
```python
def reverseString(s):
    left, right = 0, len(s) - 1
    while left < right:
        s[left], s[right] = s[right], s[left]
        left += 1
        right -= 1
```
⏱ Time: O(n) | 💾 Space: O(1)

---

## LeetCode 125 — Valid Palindrome  
⭐ Idea: Two pointers from both ends skipping non-alphanumerics.
⭐  Tip: Think of “sanitized string” + compare characters ignoring case.

**Problem:** Check if, after lowercasing and removing non-alphanumeric chars, a string reads the same backward.  
**Example:**
```python
Input: "A man, a plan, a canal: Panama"
Output: True
```
**Solution:**
```python
def isPalindrome(s):
    left, right = 0, len(s) - 1
    while left < right:
        if not s[left].isalnum():
            left += 1
            continue
        if not s[right].isalnum():
            right -= 1
            continue
        if s[left].lower() != s[right].lower():
            return False
        left += 1
        right -= 1
    return True
```
⏱ Time: O(n) | 💾 Space: O(1)

---

## LeetCode 977 — Squares of a Sorted Array  
⭐ Idea: Largest square will be at ends, so use two pointers and fill result from the back.
⭐ Tip: Squared values mess up order → fill result in reverse!

**Problem:** Given a sorted array, return a new sorted array of the squares.  
**Example:**
```python
Input: [-4,-1,0,3,10]
Output: [0,1,9,16,100]
```
**Solution:**
```python
def sortedSquares(nums):
    n = len(nums)
    result = [0] * n
    left, right = 0, n - 1
    for i in range(n-1, -1, -1):
        if abs(nums[left]) > abs(nums[right]):
            result[i] = nums[left] * nums[left]
            left += 1
        else:
            result[i] = nums[right] * nums[right]
            right -= 1
    return result
```
⏱ Time: O(n) | 💾 Space: O(n)

---

## LeetCode 680 — Valid Palindrome II  
⭐ Idea: Two pointers — if mismatch, skip either left or right and retry.
⭐ Tip: Allow one “mistake” and try both possible skips.

**Problem:** You may delete at most one character to make a string a palindrome. Return `True` if possible.  
**Example:**
```python
Input: "abca"
Output: True  # Remove 'c' -> "aba"
```
**Solution:**  
```python
def validPalindrome(s):
    def check(i, j):
        while i < j:
            if s[i] != s[j]:
                return False
            i += 1
            j -= 1
        return True

    left, right = 0, len(s) - 1
    while left < right:
        if s[left] != s[right]:
            return check(left+1, right) or check(left, right-1)
        left += 1
        right -= 1
    return True
```
⏱ Time: O(n) | 💾 Space: O(1)

---

## Remove All Elements Greater than a Threshold  
⭐ Idea: Use a slow pointer to rewrite elements ≤ threshold.
⭐ Tip: Similar to “filter” idea again — include if ≤ threshold.

**Problem:** Remove all elements in `nums` greater than a given threshold value.  
**Example:**
```python
Input: nums = [1,3,5,2,8,6], threshold = 5
Output: [1,3,5,2]
```
**Solution Placeholder:**
```python
def removeGreater(nums, threshold):
    i = 0
    for j in range(len(nums)):
        if nums[j] <= threshold:
            nums[i] = nums[j]
            i += 1
    return nums[:i]
```

---

## Skip More Than Two Duplicates  
⭐ Idea: Two pointers; compare current with nums[i-2] to allow max 2 duplicates.
⭐ Tip: “At most k duplicates” → compare with i - k.

**Problem:** Given a sorted array, keep each unique element at most twice, remove extras in-place.  
**Example:**
```python
Input: [1,1,1,2,2,3]
Output: [1,1,2,2,3]
```
**Solution Placeholder:**
```python
def removeDuplicatesII(nums):
    # TODO: implement allowing at most two duplicates
    pass
```

---
