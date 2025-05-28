# 🧠 Array/String Sorting

💡 Interview Strategy:
1) Start with built-in sort unless asked to implement your own.
2) For Linked Lists, prefer Merge Sort.
3) If the question mentions "sorted array", think of Binary Search + Sorting combo.
4) When array size is large and needs in-place sorting, Quick Sort is a go-to.
5) If a stable sort is required, avoid Quick Sort unless modified.
6) If it says “keep equal elements in order”: pick stable sort
7) If it says “don’t use extra memory”: rule out Merge Sort
8) If the problem says “sort in-place”: think Quick

---

## 🫧 Bubble Sort
Concept:
Repeatedly swap adjacent elements if they are in the wrong order.

After each full pass, the largest element "bubbles up" to its correct position.

It's like repeatedly passing through the list, pushing the biggest element to the end.

```python
def bubble_sort(arr):
    n = len(arr)
    for i in range(n):
        # Last i elements are already sorted
        for j in range(0, n - i - 1):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]  # swap
    return arr

# Example
print(bubble_sort([5, 1, 4, 2, 8]))

```
Output: [1, 2, 4, 5, 8]

Complexity:

Type	Time
Best Case	O(n) (if already sorted, with optimization)
Average Case	O(n²)
Worst Case	O(n²)
| Space Complexity | O(1) (in-place) |


## 🎯 Selection Sort
Concept:
1. Divide the array into two parts:
2. Sorted part (starts empty)
3. Unsorted part (the entire array initially)
4. Find the smallest element from the unsorted part.
5. Swap it with the first unsorted element.
6. Grow the sorted part by 1 each time.

It's like selecting the minimum and moving it to its correct place.

```python
def selection_sort(arr):
    n = len(arr)
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if arr[j] < arr[min_idx]:
                min_idx = j
        # Swap the found minimum with the first element
        arr[i], arr[min_idx] = arr[min_idx], arr[i]
    return arr

# Example
print(selection_sort([5, 1, 4, 2, 8]))
```

Complexity:

Type	Time
Best Case	O(n²)
Average Case	O(n²)
Worst Case	O(n²)
| Space Complexity | O(1) |

✅ In-place, simple to understand.


## ✍️ Insertion Sort
Concept:
1. Think like sorting a hand of playing cards 🃏:
2. Pick one card at a time.
3. Insert it into the correct place in the sorted left part.

So, at each step, the left part is always sorted!
```python
def insertion_sort(arr):
    n = len(arr)
    for i in range(1, n):
        key = arr[i]
        j = i - 1
        # Move elements greater than key to one position ahead
        while j >= 0 and arr[j] > key:
            arr[j + 1] = arr[j]
            j -= 1
        arr[j + 1] = key
    return arr

# Example
print(insertion_sort([5, 1, 4, 2, 8]))
```
Complexity:

Type	Time
Best Case	O(n) (already sorted array)
Average Case	O(n²)
Worst Case	O(n²)
| Space Complexity | O(1) |

✅ In-place, Stable (equal elements stay in order).

## 🎯 Merge Sort
Concept:
Divide and Conquer strategy.

Steps:

1. Divide the array into halves until you cannot divide anymore (single elements).
2. Merge two sorted halves into one sorted array.

```python
def merge_sort(arr):
    if len(arr) <= 1:
        return arr

    # Divide
    mid = len(arr) // 2
    left_half = merge_sort(arr[:mid])
    right_half = merge_sort(arr[mid:])

    # Merge
    return merge(left_half, right_half)

def merge(left, right):
    result = []
    i = j = 0

    # Compare and merge
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1

    # Add remaining elements
    result.extend(left[i:])
    result.extend(right[j:])
    return result

# Example
print(merge_sort([5, 1, 4, 2, 8]))
```

Complexity:

Type	Time
Best Case	O(n log n)
Average Case	O(n log n)
Worst Case	O(n log n)
| Space Complexity | O(n) |


## ⚡ Quick Sort
🎯 Concept:
Divide and Conquer (just like Merge Sort).

Choose a pivot (one element).

Partition array:

Elements smaller than pivot → left

Elements bigger than pivot → right

Recursively sort left and right parts.

In short: Pick a pivot → put it in right place → sort smaller parts.

```python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr

    pivot = arr[-1]  # picking the last element as pivot
    left = [x for x in arr[:-1] if x <= pivot]
    right = [x for x in arr[:-1] if x > pivot]

    return quick_sort(left) + [pivot] + quick_sort(right)

# Example
print(quick_sort([5, 1, 4, 2, 8]))
```
Complexity:

Type	Time
Best Case	O(n log n)
Average Case	O(n log n)
Worst Case	O(n²) (rare)
| Space Complexity | O(log n) | (stack space for recursion)

✅ In-place (optimized version), very fast!


# 🧠 Array/String Searching

1) Linear Search
2) Binary Search
3) first/last occurrence
4) Search in Rotated Array
5) Binary Search on Answer (Min/Max problems)
6) Lower/Upper Bound

---

## Linear Search (Brute Force)
Idea: Check each element one by one.

```python
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1

# Example
arr = [5, 8, 1, 3, 9]
target = 3
print(linear_search(arr, target))  # Output: 3
```
Time Complexity: O(n)
Space Complexity: O(1)

---

## Binary Search (Efficient on Sorted Arrays)

Idea:

1) Split array into halves.
2) Compare middle element with target.
3) Eliminate half each time.

```python
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
            
    return -1

# Example
arr = [1, 3, 5, 7, 9, 11]
target = 7
print(binary_search(arr, target))  # Output: 3
```
Time Complexity: O(log n)
Space Complexity: O(1)

---

# 🧠 Array/String Two Pointers
Concept:

1) This is a super versatile pattern, often used for:
2) Palindromes
3) Reversing
4) Substrings
5) Comparing characters from both ends

---

## 🔢 Easy Level Questions

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
# 🧠 Array/String Sliding Window Technique

1) subarray problem
2) find min/max within a window

Concept:

Sliding Window is used for:
1) Substrings
2) Contiguous elements
3) Fixed or dynamic range
4) Optimizing time from O(n²) → O(n)

🔧 Template for Sliding Window (Variable Window Size)
```python
left = 0
for right in range(len(s)):
    # Expand the window
    # Shrink from the left if needed
    # Update result if needed
```
---

## problem

# 🧠 Array/String Matrix

1) Rotate matrix elements
2) Magic square
3) Square of Diagonal elements

---

## Common Operations on Matrices:
1) Accessing Elements:
You access elements in a matrix using row and column indices.

```python
# Accessing element at row 2, column 3
element = matrix[1][2]  # Index starts from 0
```
2) Matrix Addition:
Two matrices of the same size can be added by adding their corresponding elements.

```python
A = [
    [1, 2],
    [3, 4]
]
B = [
    [5, 6],
    [7, 8]
]
# Matrix Addition: A + B
result = [
    [A[i][j] + B[i][j] for j in range(len(A[0]))] 
    for i in range(len(A))
]
```
Result:

```python
[
    [6, 8],
    [10, 12]
]
```
3) Matrix Multiplication:
Matrix multiplication is defined as the dot product of rows of the first matrix with columns of the second matrix.
The number of columns in the first matrix must be equal to the number of rows in the second matrix for multiplication to be valid.

```python
A = [
    [1, 2],
    [3, 4]
]
B = [
    [5, 6],
    [7, 8]
]

result = [
    [sum(A[i][k] * B[k][j] for k in range(len(A[0]))) for j in range(len(B[0]))] 
    for i in range(len(A))
]
```
Result:
```python
[
    [19, 22],
    [43, 50]
]
```
4) Transpose of a Matrix:
The transpose of a matrix is obtained by flipping it over its diagonal (i.e., rows become columns).

```python
A = [
    [1, 2],
    [3, 4]
]

# Transpose of A
result = [list(row) for row in zip(*A)]  # Using zip to transpose
```
Result:
```python
[
    [1, 3],
    [2, 4]
]
```
5) Scalar Multiplication:
In scalar multiplication, each element of the matrix is multiplied by a constant scalar value.

```python
scalar = 2
A = [
    [1, 2],
    [3, 4]
]

result = [[scalar * A[i][j] for j in range(len(A[0]))] for i in range(len(A))]
```
Result:

```python
[
    [2, 4],
    [6, 8]
]
```

---

## Matrix Rotation: Rotate a Matrix 90 Degrees Clockwise

This is a common matrix manipulation problem. The goal is to rotate a given n x n matrix by 90 degrees in place.

Approach:
1) To rotate the matrix 90 degrees clockwise, you can either:
2) Transpose the matrix, which swaps rows and columns.
3) Reverse each row of the transposed matrix to get the final rotated matrix.

Solution:
```python
def rotate(matrix):
    n = len(matrix)
    
    # Step 1: Transpose the matrix
    for i in range(n):
        for j in range(i, n):
            matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
    
    # Step 2: Reverse each row
    for i in range(n):
        matrix[i].reverse()

    return matrix
```
Example:
Input:
```python
[
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
```
Output:
```python
[
    [7, 4, 1],
    [8, 5, 2],
    [9, 6, 3]
]
```

---

## Spiral Order Matrix
Given an m x n matrix, we need to return all its elements in spiral order. The spiral order means you start from the top-left corner and traverse the matrix in a circular fashion (right -> down -> left -> up).

Approach:
1) Use four pointers (top, bottom, left, right) to represent the boundaries of the matrix.
2) Traverse the matrix in a spiral pattern while shrinking the boundaries.

Solution:
```python
def spiralOrder(matrix):
    result = []
    while matrix:
        result += matrix.pop(0)  # Pop the top row
        if matrix and matrix[0]:
            for row in matrix:
                result.append(row.pop())  # Pop the right column
        if matrix:
            result += matrix.pop()[::-1]  # Pop the bottom row (reversed)
        if matrix and matrix[0]:
            for row in matrix[::-1]:
                result.append(row.pop(0))  # Pop the left column
    return result
```
Example:
Input:
```python
[
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
```
Output:
```python
[1, 2, 3, 6, 9, 8, 7, 4, 5]
```

---

### Diagonal Sum of Matrix
Given a square matrix, calculate the sum of its diagonals.

Approach:
1) The primary diagonal consists of elements where i == j.
2) The secondary diagonal consists of elements where i + j == n - 1 (for an n x n matrix).
3) Be careful not to double count the center element if the matrix size is odd.

Solution:
```python
def diagonalSum(matrix):
    n = len(matrix)
    total_sum = 0
    
    for i in range(n):
        total_sum += matrix[i][i]  # Primary diagonal
        total_sum += matrix[i][n - i - 1]  # Secondary diagonal
    
    if n % 2 == 1:  # If the matrix size is odd, subtract the center element (counted twice)
        total_sum -= matrix[n // 2][n // 2]
    
    return total_sum
```
Example:
Input:
```python
[
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
```
Output:
```python
25  # (1 + 5 + 9 + 3 + 7)
```

---

## Check if a Matrix is an Identity Matrix

An identity matrix is a square matrix where:
1) All the elements in the main diagonal are 1.
2) All the other elements are 0.

Approach:
Check if every element on the main diagonal is 1, and every off-diagonal element is 0.

Solution:
```python
def isIdentity(matrix):
    n = len(matrix)
    for i in range(n):
        for j in range(n):
            if (i == j and matrix[i][j] != 1) or (i != j and matrix[i][j] != 0):
                return False
    return True
```
Example:
Input:
```python
[
    [1, 0, 0],
    [0, 1, 0],
    [0, 0, 1]
]
```
Output:
```python
True
```

---

## Matrix Multiplication
Matrix multiplication is a fundamental concept in linear algebra. The result of multiplying an A (m x n) matrix by a B (n x p) matrix is a new matrix C (m x p).

Approach:
For each element in the result matrix, calculate the dot product of the corresponding row in A and column in B.

Solution:
```python
def multiply(A, B):
    m, n = len(A), len(A[0])  # Dimensions of A
    n_b, p = len(B), len(B[0])  # Dimensions of B

    if n != n_b:  # Matrix multiplication is only possible if n == n_b
        return []

    # Initialize result matrix with zero values
    result = [[0] * p for _ in range(m)]

    for i in range(m):
        for j in range(p):
            for k in range(n):
                result[i][j] += A[i][k] * B[k][j]
    
    return result
```
Example:
Input:
```python
A = [
    [1, 2],
    [3, 4]
]
B = [
    [5, 6],
    [7, 8]
]
```
Output:
```python
[
    [19, 22],
    [43, 50]
]
```

---

## Square of Diagonal Elements

To compute the **square of diagonal elements** in a matrix, we can break it down into a few steps:

Problem Statement:
Given an `n x n` matrix, find the **sum of squares of all elements on the primary diagonal**.

✅ Primary Diagonal Only

Example:
```python
[
 [1, 2, 3],
 [4, 5, 6],
 [7, 8, 9]
]
```

Primary diagonal: `1, 5, 9` → Squares: `1, 25, 81` → Sum: `107`

```python
def square_of_primary_diagonal(matrix):
    total = 0
    for i in range(len(matrix)):
        total += matrix[i][i] ** 2
    return total
```

✅ Both Diagonals

If you want **squares of both diagonals**, and to avoid double-counting the center (in odd-sized matrices):

```python
def square_of_both_diagonals(matrix):
    n = len(matrix)
    total = 0
    for i in range(n):
        total += matrix[i][i] ** 2  # Primary diagonal
        total += matrix[i][n - i - 1] ** 2  # Secondary diagonal
    
    if n % 2 == 1:
        center = matrix[n // 2][n // 2]
        total -= center ** 2  # Center was added twice

    return total
```

---

## Magic Square

---

# 🧠 Array/String Hashmaps

Hashmaps (also known as dictionaries in Python) are a powerful tool for solving problems related to arrays and strings, especially when we need to track frequencies, find duplicates, or implement lookups efficiently.

---

## Frequency Counting in Strings or Arrays
A common use of hashmaps is to count the frequency of each element in a string or an array.

Example: Count Characters in a String
Problem: Given a string, count the frequency of each character.

```python
def count_characters(s: str):
    char_count = {}
    for char in s:
        if char in char_count:
            char_count[char] += 1
        else:
            char_count[char] = 1
    return char_count

# Example usage:
s = "apple"
print(count_characters(s))
```
Output:
```python
{'a': 1, 'p': 2, 'l': 1, 'e': 1}
```

---

## Two Sum Problem (Using Hashmap)
This is a classic problem that can be efficiently solved using a hashmap.

Problem: Given an array of integers, return the indices of the two numbers that add up to a specific target.

```python
def two_sum(nums, target):
    num_dict = {}
    for i, num in enumerate(nums):
        complement = target - num
        if complement in num_dict:
            return [num_dict[complement], i]
        num_dict[num] = i
    return []

# Example usage:
nums = [2, 7, 11, 15]
target = 9
print(two_sum(nums, target))
```
Output:
```python
[0, 1]
```

---

## Longest Substring Without Repeating Characters
This is a common sliding window problem, and hashmaps are helpful to track the last index of each character seen.

Problem: Given a string, find the length of the longest substring without repeating characters.

```python
def length_of_longest_substring(s: str):
    char_map = {}
    left = 0
    max_length = 0
    
    for right in range(len(s)):
        if s[right] in char_map and char_map[s[right]] >= left:
            left = char_map[s[right]] + 1
        char_map[s[right]] = right
        max_length = max(max_length, right - left + 1)
    
    return max_length

# Example usage:
s = "abcabcbb"
print(length_of_longest_substring(s))
```
Output:
```python
3  # "abc" is the longest substring
```

---

## Check for Anagram
Hashmaps can be used to determine if two strings are anagrams of each other by counting the frequency of characters.

Problem: Given two strings, return True if they are anagrams of each other, otherwise return False.

```python
def are_anagrams(s1: str, s2: str):
    if len(s1) != len(s2):
        return False
    
    char_count = {}
    
    for char in s1:
        char_count[char] = char_count.get(char, 0) + 1
    
    for char in s2:
        if char_count.get(char, 0) == 0:
            return False
        char_count[char] -= 1
    
    return True

# Example usage:
s1 = "anagram"
s2 = "nagaram"
print(are_anagrams(s1, s2))
```
Output:
```python
True
```

---

## Subarray Sum Equals K (Hashmap-based Approach)
Problem: Given an array of integers and an integer k, find the total number of continuous subarrays whose sum equals k.

```python
def subarray_sum(nums, k):
    prefix_sum = 0
    count = 0
    sum_map = {0: 1}  # Base case: one way to have sum 0 (empty subarray)
    
    for num in nums:
        prefix_sum += num
        if prefix_sum - k in sum_map:
            count += sum_map[prefix_sum - k]
        
        sum_map[prefix_sum] = sum_map.get(prefix_sum, 0) + 1
    
    return count

# Example usage:
nums = [1, 2, 3]
k = 3
print(subarray_sum(nums, k))
```
Output:
```python
2  # Subarrays [1, 2] and [3] sum to 3
```

---

## Find All Duplicates in an Array
This problem can be solved by counting how many times each element appears in the array using a hashmap.

Problem: Given an integer array, return all the elements that appear twice or more.

```python
def find_duplicates(nums):
    num_count = {}
    duplicates = []
    
    for num in nums:
        if num in num_count:
            num_count[num] += 1
        else:
            num_count[num] = 1
    
    for num, count in num_count.items():
        if count > 1:
            duplicates.append(num)
    
    return duplicates

# Example usage:
nums = [4, 3, 2, 7, 8, 2, 3, 1]
print(find_duplicates(nums))
```
Output:
```python
[3, 2]
```

---

## Top K Frequent Elements
In this problem, a hashmap is used to store the frequency of each element, and we need to find the top k most frequent elements.

Problem: Given an array of integers, return the k most frequent elements.

```python
from collections import Counter

def top_k_frequent(nums, k):
    count = Counter(nums)
    return [item[0] for item in count.most_common(k)]

# Example usage:
nums = [1, 1, 1, 2, 2, 3]
k = 2
print(top_k_frequent(nums, k))
```
Output:
```python
[1, 2]
```

---

## Group Anagrams
In this problem, we use a hashmap to group anagrams together by sorting the characters of each string as the key.

Problem: Given an array of strings, group the anagrams together.

```python
from collections import defaultdict

def group_anagrams(strs):
    anagram_map = defaultdict(list)
    
    for s in strs:
        sorted_str = ''.join(sorted(s))
        anagram_map[sorted_str].append(s)
    
    return list(anagram_map.values())

# Example usage:
strs = ["eat", "tea", "tan", "ate", "nat", "bat"]
print(group_anagrams(strs))
```
Output:
```python
[['eat', 'tea', 'ate'], ['tan', 'nat'], ['bat']]
```

---

## Find the Majority Element
The majority element in an array is the element that appears more than n/2 times.

Problem: Given an integer array, find the majority element.

```python
from collections import Counter

def majority_element(nums):
    count = Counter(nums)
    return max(count, key=count.get)

# Example usage:
nums = [3, 2, 3]
print(majority_element(nums))
```
Output:
```python
3
```

---
