
# Gaussian Elimination Solver in Python

This project implements **Gaussian Elimination** from scratch using **NumPy** to solve systems of linear equations of the form:

AX = B

Rather than using built-in solvers like `numpy.linalg.solve()`, this notebook provides a step-by-step breakdown of the Gaussian Elimination process, helping you understand the underlying math and logic.

---

## What the Notebook Covers

1. Swapping rows in a matrix for pivoting  
2. Finding the first non-zero element in a column or row  
3. Reducing a matrix to **Row Echelon Form (REF)**  
4. Performing **Back Substitution** to solve the system  
5. Wrapping all logic in one function: `gaussian_elimination()`

---

## Helper Functions

### 1. `swap_rows(M, row1, row2)`

Swaps two rows in a matrix using NumPy's row indexing.

**Parameters:**
- `M` (numpy.array): The matrix
- `row1` (int): Index of first row
- `row2` (int): Index of second row

**Example:**
```python
A = np.array([[1, 2], [3, 4]])
swap_rows(A, 0, 1)
# Output: [[3, 4], [1, 2]]
```

---

### 2. `get_index_first_non_zero_from_column(M, column, starting_row)`

Finds the index of the first non-zero value in a column from a starting row downwards.

**Example:**
```python
M = np.array([
    [0, 0, 0],
    [0, 5, 0],
    [0, 0, 9]
])
get_index_first_non_zero_from_column(M, column=1, starting_row=0)
# Output: 1
```

---

### 3. `get_index_first_non_zero_from_row(M, row, augmented=False)`

Finds the first non-zero value in a row.  
If `augmented=True`, it skips the last column (usually constants).

---

### 4. `augmented_matrix(A, B)`

Creates an augmented matrix by stacking matrix A and vector B horizontally.

**Example:**
```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5], [6]])
augmented_matrix(A, B)
# Output:
# [[1, 2, 5],
#  [3, 4, 6]]
```

---

## Main Algorithm Functions

### 5. `row_echelon_form(A, B)`

Reduce the augmented matrix `[A | B]` into Row Echelon Form using Gaussian elimination.

- Swaps rows if needed  
- Normalises pivots  
- Eliminates values below the pivot  

**Returns:**
- A matrix in row echelon form if it is solvable  
- `'singular system'` if the system is not solvable  

---

### 6. `back_substitution(M)`

Takes a matrix in row echelon form and performs back substitution.

- Works from bottom row up  
- Eliminates entries above pivots  
- Extracts the solution vector  

**Returns:**
- A NumPy array containing the solution values  

---

### 7. `gaussian_elimination(A, B)`

Wraps both `row_echelon_form()` and `back_substitution()` together to solve the entire linear system.

**Returns:**
- The final solution vector  
- Or `'singular system'` if the matrix is not invertible  

---

## Example: Solving a Linear System

Solving the system:

```
2x + y - z = 8  
-3x - y + 2z = -11  
-2x + y + 2z = -3
```

**Code:**
```python
import numpy as np

A = np.array([
    [2, 1, -1],
    [-3, -1, 2],
    [-2, 1, 2]
])
B = np.array([
    [8],
    [-11],
    [-3]
])

solution = gaussian_elimination(A, B)
print(solution)

# Output: [2. 3. -1.]
```

---

## Requirements

- Python 3.x  
- NumPy  
- Jupyter Notebook (recommended)

---

## File Structure

- `notebook.ipynb`: Full walkthrough with explanations  
- `README.md`: Project description  

---

## License

This project is open-source and free to use under the MIT License.
