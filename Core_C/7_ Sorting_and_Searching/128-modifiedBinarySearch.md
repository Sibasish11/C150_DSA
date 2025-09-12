# Write a program to find the first occurrence of an element in a sorted array with duplicates using a modified Binary Search.

```c

#include <stdio.h>

// Function to find the first occurrence of a key using Binary Search
int firstOccurrence(int arr[], int n, int key) {
    int low = 0, high = n - 1, result = -1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == key) {
            result = mid;      // store index
            high = mid - 1;    // continue search on left side
        }
        else if (arr[mid] < key) {
            low = mid + 1;     // search right half
        }
        else {
            high = mid - 1;    // search left half
        }
    }
    return result;
}

// Function to print the result
int main() {
    int arr[] = {1, 2, 4, 4, 4, 5, 6, 7};
    int n = sizeof(arr) / sizeof(arr[0]);
    int key = 4;

    int index = firstOccurrence(arr, n, key);

    if (index != -1)
        printf("First occurrence of %d is at index %d\n", key, index);
    else
        printf("%d not found in the array\n", key);

    return 0;
}


```

## Output:

```c

First occurrence of 4 is at index 2

```
