# Write a program that demonstrates an O(N^2) time complexity operation (e.g., finding all pairs in an array). Explain why it's O(N^2) in comments.

```c
#include <stdio.h>

int main() {
    int arr[] = {1, 2, 3, 4};
    int n = sizeof(arr) / sizeof(arr[0]);

    // Finding all pairs requires two nested loops
    // Outer loop runs N times, and for each iteration,
    // the inner loop also runs up to N times.
    // Total operations ~ N * N = N^2 (quadratic growth)
    printf("All pairs in the array:\n");
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            printf("(%d, %d)\n", arr[i], arr[j]);
        }
    }

    return 0;
}

```

## Output:
```c

All pairs in the array:
(1, 1)
(1, 2)
(1, 3)
(1, 4)
(2, 1)
(2, 2)
(2, 3)
(2, 4)
(3, 1)
(3, 2)
(3, 3)
(3, 4)
(4, 1)
(4, 2)
(4, 3)
(4, 4)

```
