# Develop a program to count inversions in an array using a modified Merge Sort.

```c

#include <stdio.h>

// Merge function to count inversions
long long mergeAndCount(int arr[], int temp[], int left, int mid, int right) {
    int i = left;     // left subarray index
    int j = mid + 1;  // right subarray index
    int k = left;     // merged array index
    long long invCount = 0;

    while (i <= mid && j <= right) {
        if (arr[i] <= arr[j]) {
            temp[k++] = arr[i++];
        } else {
            temp[k++] = arr[j++];
            invCount += (mid - i + 1); // count inversions
        }
    }

    // Copy remaining elements
    while (i <= mid) {
        temp[k++] = arr[i++];
    }
    while (j <= right) {
        temp[k++] = arr[j++];
    }

    // Copy back to original array
    for (i = left; i <= right; i++) {
        arr[i] = temp[i];
    }

    return invCount;
}

// Recursive function to count inversions
long long mergeSortAndCount(int arr[], int temp[], int left, int right) {
    long long invCount = 0;

    if (left < right) {
        int mid = (left + right) / 2;

        invCount += mergeSortAndCount(arr, temp, left, mid);
        invCount += mergeSortAndCount(arr, temp, mid + 1, right);

        invCount += mergeAndCount(arr, temp, left, mid, right);
    }

    return invCount;
}

int main() {
    int arr[] = {2, 4, 1, 3, 5};
    int n = sizeof(arr) / sizeof(arr[0]);
    int temp[n];

    long long invCount = mergeSortAndCount(arr, temp, 0, n - 1);

    printf("Number of inversions = %lld\n", invCount);

    return 0;
}


```

## Sample Output

```c

Number of inversions = 3

```
