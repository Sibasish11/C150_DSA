# Implement a program to find the ceiling (smallest element greater than or equal to target) of an element in a sorted array.

```c

#include <stdio.h>

// Function to find ceiling using Binary Search
int findCeil(int arr[], int n, int key) {
    int low = 0, high = n - 1, result = -1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == key) {
            return arr[mid]; // exact match is the ceil
        }
        else if (arr[mid] < key) {
            low = mid + 1; // move right to find bigger element
        }
        else {
            result = arr[mid]; // possible ceil
            high = mid - 1;    // try to find smaller ceil
        }
    }
    return result;
}

int main() {
    int arr[] = {1, 2, 4, 6, 10, 12, 14};
    int n = sizeof(arr) / sizeof(arr[0]);
    int key = 5;

    int ceilVal = findCeil(arr, n, key);

    if (ceilVal != -1)
        printf("Ceiling of %d is %d\n", key, ceilVal);
    else
        printf("No ceiling exists for %d\n", key);

    return 0;
}


```

## Sample Output:

```c

Ceiling of 5 is 6

```
