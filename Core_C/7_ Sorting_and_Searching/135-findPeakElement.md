# Implement a program to find the peak element in an array (an element greater than its neighbors).

```c

#include <stdio.h>

// Function to find a peak element index

int findPeakElement(int arr[], int n) {
    int low = 0, high = n - 1;

    while (low < high) {
        int mid = low + (high - low) / 2;

        // If mid element is less than the next, peak lies on the right
        if (arr[mid] < arr[mid + 1])
            low = mid + 1;
        else
            high = mid; // Peak lies on left (including mid)
    }
    return low; // or high, both are same here
}

int main() {
    int arr[] = {1, 3, 20, 4, 1, 0};
    int n = sizeof(arr) / sizeof(arr[0]);

    int peakIndex = findPeakElement(arr, n);
    printf("Peak element is %d at index %d\n", arr[peakIndex], peakIndex);

    return 0;
}


```

## Example Run

- For array:

```c

[1, 3, 20, 4, 1, 0]

```

- Output:

```c

Peak element is 20 at index 2

```
