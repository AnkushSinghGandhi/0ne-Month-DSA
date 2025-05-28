# 🧠 Sorting

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
1) Repeatedly swap adjacent elements if they are in the wrong order.
2) After each full pass, the largest element "bubbles up" to its correct position.
3) It's like repeatedly passing through the list, pushing the biggest element to the end.

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

1) Choose a pivot (one element).
2) Partition array:
   a) Elements smaller than pivot → left
   b) Elements bigger than pivot → right
3) Recursively sort left and right parts.

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
