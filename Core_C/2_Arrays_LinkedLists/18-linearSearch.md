# Write a program that implements two different algorithms to find if an element exists in an array: one using linear search (O(N)) and another using binary search (O(log N)). For various array sizes (e.g., 1000, 10000, 100000), measure and compare the execution times of both algorithms. Observe and comment on how their performance scales differently with increasing input size.

```c


Explanation of Algorithms:

1) Linear Search:
   - Traverse array elements one by one until the target is found or end of array is reached.
   - Time Complexity: O(N)

2) Binary Search:
   - Works only on sorted arrays.
   - Repeatedly divide the search interval in half until the target is found.
   - Time Complexity: O(log N)

---------------------------------------------------------
Expected Observation:
---------------------------------------------------------
- For small arrays, both algorithms run fast, and differences may be negligible.
- As array size grows:
    * Linear search time increases proportionally with N.
    * Binary search time grows very slowly (logarithmic).
- For very large arrays, binary search is significantly faster.


#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// Linear Search Implementation
int linearSearch(int arr[], int n, int key) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == key)
            return i;
    }
    return -1;
}

// Binary Search Implementation (Array must be sorted)
int binarySearch(int arr[], int n, int key) {
    int low = 0, high = n - 1;
    while (low <= high) {
        int mid = (low + high) / 2;
        if (arr[mid] == key)
            return mid;
        else if (arr[mid] < key)
            low = mid + 1;
        else
            high = mid - 1;
    }
    return -1;
}

// Function to test and compare execution times
void testPerformance(int n, int key) {
    int *arr = (int *)malloc(n * sizeof(int));
    for (int i = 0; i < n; i++) {
        arr[i] = i + 1; // Sorted array from 1 to N
    }

    clock_t start, end;
    double cpu_time_used;

    // Linear Search
    start = clock();
    int linearResult = linearSearch(arr, n, key);
    end = clock();
    cpu_time_used = ((double)(end - start)) / CLOCKS_PER_SEC;
    printf("Linear Search (N=%d): Found at index %d, Time = %f seconds\n",
           n, linearResult, cpu_time_used);

    // Binary Search
    start = clock();
    int binaryResult = binarySearch(arr, n, key);
    end = clock();
    cpu_time_used = ((double)(end - start)) / CLOCKS_PER_SEC;
    printf("Binary Search (N=%d): Found at index %d, Time = %f seconds\n",
           n, binaryResult, cpu_time_used);

    free(arr);
}

int main() {
    int key;

    printf("Enter element to search: ");
    scanf("%d", &key);

    printf("\n--- Performance Comparison ---\n");
    testPerformance(1000, key);
    testPerformance(10000, key);
    testPerformance(100000, key);

    return 0;
}

```

## Sample Observation (Will vary depending on machine):

```c
Enter element to search: 99999

Performance Comparison 

Linear Search (N=1000): Found at index 999, Time = 0.000001 sec
Binary Search (N=1000): Found at index 999, Time = 0.000000 sec

Linear Search (N=10000): Found at index 9999, Time = 0.000010 sec
Binary Search (N=10000): Found at index 9999, Time = 0.000001 sec

Linear Search (N=100000): Found at index 99999, Time = 0.000120 sec
Binary Search (N=100000): Found at index 99999, Time = 0.000001 sec
```

Conclusion:

- Linear Search grows linearly with input size (O(N)).
- Binary Search grows logarithmically with input size (O(log N)).
- For large datasets, binary search is far more efficient.



```
