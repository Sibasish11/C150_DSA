# Compare the time complexities of Quick, Merge, and Heap Sort. (Conceptual, in comments).

## Comparison of Quick Sort, Merge Sort, and Heap Sort

### 1️⃣ Quick Sort
   - Best Case: O(n log n)   (balanced partition)
   - Average Case: O(n log n)
   - Worst Case: O(n^2)      (highly unbalanced partition, e.g., sorted input with poor pivot choice)
   - Space Complexity: O(log n)  (recursion stack)
   - Stability: Not stable
   - Notes: Very fast in practice due to good cache performance.
            With randomized or median-of-three pivot selection, 
            worst case rarely occurs.

### 2️⃣ Merge Sort
   - Best Case: O(n log n)
   - Average Case: O(n log n)
   - Worst Case: O(n log n)  (guaranteed)
   - Space Complexity: O(n)  (needs auxiliary arrays for merging)
   - Stability: Stable
   - Notes: Preferred for linked lists and external sorting 
            (sorting data from disk). Predictable runtime.

### 3️⃣ Heap Sort
   - Best Case: O(n log n)
   - Average Case: O(n log n)
   - Worst Case: O(n log n)
   - Space Complexity: O(1)  (in-place)
   - Stability: Not stable
   - Notes: Guarantees O(n log n), but usually slower than Quick Sort 
            in practice due to poor cache performance.


#### 📌 Summary:
- Quick Sort: Fastest in practice, but O(n^2) in worst case.
- Merge Sort: Always O(n log n), stable, but uses extra space.
- Heap Sort: O(n log n) always, in-place, but not stable 
             and slower than Quick Sort in real-world usage.

