# 🧠 Searching

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
