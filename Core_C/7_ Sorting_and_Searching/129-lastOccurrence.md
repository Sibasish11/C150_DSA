# Implement a program to find the last occurrence of an element in a sorted array with duplicates using a modified Binary Search.

```c

#include <stdio.h>

// Function to find the last occurrence of a key using Binary Search
int lastOccurrence(int arr[], int n, int key) {
    int low = 0, high = n - 1, result = -1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == key) {
            result = mid;      // store index
            low = mid + 1;     // continue search on right side
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

int main() {
    int arr[] = {1, 2, 4, 4, 4, 5, 6, 7};
    int n = sizeof(arr) / sizeof(arr[0]);
    int key = 4;

    int index = lastOccurrence(arr, n, key);

    if (index != -1)
        printf("Last occurrence of %d is at index %d\n", key, index);
    else
        printf("%d not found in the array\n", key);

    return 0;
}


```

## Sample Output:

```c

Last occurrence of 4 is at index 4

```
