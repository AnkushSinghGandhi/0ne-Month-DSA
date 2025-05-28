# 🧠 Matrices

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
