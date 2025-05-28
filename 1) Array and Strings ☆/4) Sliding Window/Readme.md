# 🧠 Sliding Window Technique

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
