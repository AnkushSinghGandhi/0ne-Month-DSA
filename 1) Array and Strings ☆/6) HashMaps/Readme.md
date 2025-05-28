# 🧠 Hashmaps

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
