# Implement Binary Search (iterative) to find an element in a sorted array. Analyze its time complexity.

```c

#include <stdio.h>

// Function to perform Iterative Binary Search
int binarySearch(int arr[], int n, int key) {
    int low = 0, high = n - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2; // to prevent overflow

        if (arr[mid] == key) {
            return mid; // element found
        } 
        else if (arr[mid] < key) {
            low = mid + 1; // search right half
        } 
        else {
            high = mid - 1; // search left half
        }
    }

    return -1; // not found
}

int main() {
    int arr[] = {5, 15, 25, 35, 45, 55, 65};
    int n = sizeof(arr) / sizeof(arr[0]);
    int key = 45;

    int result = binarySearch(arr, n, key);

    if (result != -1) {
        printf("Element %d found at index %d\n", key, result);
    } else {
        printf("Element %d not found in the array\n", key);
    }

    return 0;
}


```

## Example Output:

```c

Element 45 found at index 4

```
