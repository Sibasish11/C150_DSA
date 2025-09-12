# Compare the time complexities of Bubble, Selection, and Insertion Sort. (Conceptual, in comments).


## Comparison of Bubble Sort, Selection Sort, and Insertion Sort


### 1️⃣ Bubble Sort
   - Best Case: O(n)       (when array is already sorted, optimized with swap flag)
   - Average Case: O(n^2)
   - Worst Case: O(n^2)
   - Space Complexity: O(1)  (in-place)
   - Stability: Stable
   - Notes: Simple to implement, inefficient for large arrays.

### 2️⃣ Selection Sort
   - Best Case: O(n^2)   (no early termination, always scans full array)
   - Average Case: O(n^2)
   - Worst Case: O(n^2)
   - Space Complexity: O(1)  (in-place)
   - Stability: Not stable (swaps may change equal elements’ order)
   - Notes: Does fewer swaps than Bubble Sort (max n-1 swaps).

### 3️⃣ Insertion Sort
   - Best Case: O(n)       (already sorted array → only one comparison per element)
   - Average Case: O(n^2)
   - Worst Case: O(n^2)    (reverse sorted array → max shifts)
   - Space Complexity: O(1)  (in-place)
   - Stability: Stable
   - Notes: Efficient for small or nearly sorted arrays.

##### 📌 Summary:
- Bubble Sort and Insertion Sort can achieve O(n) in the best case 
  (with optimization), but Selection Sort is always O(n^2).
- Insertion Sort is generally more practical than Bubble/Selection 
  for small or nearly sorted data.
- All three are inefficient for large datasets (compared to O(n log n) algorithms).
