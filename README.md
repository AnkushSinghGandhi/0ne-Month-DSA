
# 🧠 Array/String Two Pointers & More

---

## 🔢 Easy Level Questions

### LeetCode 1 — Two Sum  
**Problem:** Given an array of integers and a target, return the indices of the two numbers that add up to the target.  
**Example:**
```python
Input: nums = [2, 7, 11, 15], target = 9  
Output: [0, 1]
```
**Solution (HashMap):**
```python
def twoSum(nums, target):
    hashmap = {}
    for i, num in enumerate(nums):
        diff = target - num
        if diff in hashmap:
            return [hashmap[diff], i]
        hashmap[num] = i
```
⏱ Time: O(n) | 💾 Space: O(n)

---

### LeetCode 20 — Valid Parentheses  
**Problem:** Given a string containing `()[]{}`, determine if it’s valid (correctly closed & nested).  
**Example:**
```python
Input: s = "()[]{}"
Output: True
```
**Solution:**
```python
def isValid(s):
    stack = []
    mapping = {")":"(", "}":"{", "]":"["}
    for char in s:
        if char not in mapping:
            stack.append(char)
        else:
            if not stack or stack[-1] != mapping[char]:
                return False
            stack.pop()
    return not stack
```
⏱ Time: O(n) | 💾 Space: O(n)

---

### LeetCode 26 — Remove Duplicates from Sorted Array  
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

### LeetCode 27 — Remove Element  
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

### LeetCode 283 — Move Zeroes  
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

### LeetCode 344 — Reverse String  
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

### LeetCode 125 — Valid Palindrome  
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

### LeetCode 977 — Squares of a Sorted Array  
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

### LeetCode 680 — Valid Palindrome II  
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

### Remove All Elements Greater than a Threshold  
**Problem:** Remove all elements in `nums` greater than a given threshold value.  
**Example:**
```python
Input: nums = [1,3,5,2,8,6], threshold = 5
Output: [1,3,5,2]
```
**Solution Placeholder:**
```python
def removeGreater(nums, threshold):
    # TODO: implement in-place removal
    pass
```

---

### Skip More Than Two Duplicates  
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

## 🔥 Medium Level Questions

### LeetCode 11 — Container With Most Water  
*(Solved above)*

### LeetCode 15 — 3Sum  
*(Solved above)*

### LeetCode 167 — Two Sum II – Input Array Is Sorted  
**Problem:** 1-indexed sorted array, find two numbers that add up to target.  
**Example:**
```python
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
```
**Solution:**
```python
def twoSumII(numbers, target):
    i, j = 0, len(numbers) - 1
    while i < j:
        s = numbers[i] + numbers[j]
        if s == target:
            return [i+1, j+1]
        elif s < target:
            i += 1
        else:
            j -= 1
```

---

### LeetCode 75 — Sort Colors  
**Problem:** Sort array of 0s,1s,2s in-place (Dutch National Flag).  
**Example:**
```python
Input: [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
```
**Solution:**
```python
def sortColors(nums):
    low, mid, high = 0, 0, len(nums) - 1
    while mid <= high:
        if nums[mid] == 0:
            nums[low], nums[mid] = nums[mid], nums[low]
            low += 1
            mid += 1
        elif nums[mid] == 1:
            mid += 1
        else:
            nums[mid], nums[high] = nums[high], nums[mid]
            high -= 1
```

---

### LeetCode 209 — Minimum Size Subarray Sum  
**Problem:** Smallest length of contiguous subarray with sum ≥ target.  
**Example:**
```python
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2  # [4,3]
```
**Solution Placeholder:**
```python
def minSubArrayLen(target, nums):
    # TODO: implement sliding window
    pass
```

---

### LeetCode 438 — Find All Anagrams in a String  
**Problem:** Find start indices of p's anagrams in s.  
**Example:**
```python
Input: s = "cbaebabacd", p = "abc"
Output: [0,6]
```
**Solution Placeholder:**
```python
def findAnagrams(s, p):
    # TODO: implement sliding window + frequency map
    pass
```

---

### LeetCode 713 — Subarray Product Less Than K  
**Problem:** Number of contiguous subarrays where product < k.  
**Example:**
```python
Input: nums = [10,5,2,6], k = 100
Output: 8
```
**Solution Placeholder:**
```python
def numSubarrayProductLessThanK(nums, k):
    # TODO: implement two-pointer sliding window
    pass
```

---

### LeetCode 658 — Find K Closest Elements  
**Problem:** Return k closest elements to x in sorted array.  
**Example:**
```python
Input: arr = [1,2,3,4,5], k = 4, x = 3
Output: [1,2,3,4]
```
**Solution Placeholder:**
```python
def findClosestElements(arr, k, x):
    # TODO: implement two-pointer or binary search
    pass
```
