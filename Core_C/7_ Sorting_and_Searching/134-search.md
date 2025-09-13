# Write a program to search for an element in a rotated sorted array.

```c

#include <stdio.h>

// Function to search in rotated sorted array

int search(int arr[], int n, int target) {
    int low = 0, high = n - 1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == target)
            return mid;

        // Check if left half is sorted
        if (arr[low] <= arr[mid]) {
            if (target >= arr[low] && target < arr[mid])
                high = mid - 1;
            else
                low = mid + 1;
        }
        // Otherwise, right half is sorted
        else {
            if (target > arr[mid] && target <= arr[high])
                low = mid + 1;
            else
                high = mid - 1;
        }
    }
    return -1; // Element not found
}

int main() {
    int arr[] = {4, 5, 6, 7, 0, 1, 2};
    int n = sizeof(arr) / sizeof(arr[0]);
    int target = 0;

    int index = search(arr, n, target);
    if (index != -1)
        printf("Element %d found at index %d\n", target, index);
    else
        printf("Element %d not found\n", target);

    return 0;
}


```

## Example Run

- Input array:

```c

arr = [4, 5, 6, 7, 0, 1, 2]
target = 0

```

## Output:

```c

Element 0 found at index 4

```
