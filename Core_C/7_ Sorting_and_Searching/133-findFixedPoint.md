# Develop a program to find a fixed point (an index i such that arr[i] == i) in a sorted array.

```c

#include <stdio.h>

// Function to find fixed point using Binary Search
int findFixedPoint(int arr[], int n) {
    int low = 0, high = n - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == mid) {
            return mid;  // found fixed point
        }
        else if (arr[mid] < mid) {
            low = mid + 1;  // move right
        }
        else {
            high = mid - 1; // move left
        }
    }
    return -1;  // no fixed point
}

int main() {
    int arr[] = {-10, -5, 0, 3, 7, 9, 12, 17};
    int n = sizeof(arr) / sizeof(arr[0]);

    int result = findFixedPoint(arr, n);

    if (result != -1)
        printf("Fixed point found at index %d (arr[%d] = %d)\n", result, result, arr[result]);
    else
        printf("No fixed point found in the array\n");

    return 0;
}

```

## Sample Output:

```c

Fixed point found at index 3 (arr[3] = 3)

```
