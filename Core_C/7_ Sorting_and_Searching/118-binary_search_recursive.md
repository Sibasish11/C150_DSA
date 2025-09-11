# Implement Binary Search (recursive) to find an element in a sorted array.

```c

#include <stdio.h>

// Recursive function for Binary Search
int binarySearchRecursive(int arr[], int low, int high, int key) {
    if (low > high) {
        return -1; // element not found
    }

    int mid = low + (high - low) / 2;

    if (arr[mid] == key) {
        return mid; // element found
    } 
    else if (arr[mid] > key) {
        return binarySearchRecursive(arr, low, mid - 1, key); // search left half
    } 
    else {
        return binarySearchRecursive(arr, mid + 1, high, key); // search right half
    }
}

int main() {
    int arr[] = {5, 15, 25, 35, 45, 55, 65};
    int n = sizeof(arr) / sizeof(arr[0]);
    int key = 35;

    int result = binarySearchRecursive(arr, 0, n - 1, key);

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

Element 35 found at index 3

```
