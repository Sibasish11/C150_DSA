# Write a program to find the floor (largest element less than or equal to target) of an element in a sorted array.

```c

#include <stdio.h>

// Function to find floor using Binary Search
int findFloor(int arr[], int n, int key) {
    int low = 0, high = n - 1, result = -1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == key) {
            return arr[mid]; // exact match is the floor
        }
        else if (arr[mid] < key) {
            result = arr[mid]; // possible floor
            low = mid + 1;     // try to find a bigger floor
        }
        else {
            high = mid - 1;    // move left
        }
    }
    return result;
}

int main() {
    int arr[] = {1, 2, 4, 6, 10, 12, 14};
    int n = sizeof(arr) / sizeof(arr[0]);
    int key = 5;

    int floorVal = findFloor(arr, n, key);

    if (floorVal != -1)
        printf("Floor of %d is %d\n", key, floorVal);
    else
        printf("No floor exists for %d\n", key);

    return 0;
}


```

## Sample Output:

```c

Floor of 5 is 4

```
