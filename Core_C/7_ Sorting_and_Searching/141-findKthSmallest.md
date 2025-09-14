# Implement a program to find the kth smallest element in two sorted arrays.

```c

#include <stdio.h>

// Function to find kth smallest element in two sorted arrays
int findKthSmallest(int arr1[], int n1, int arr2[], int n2, int k) {
    int i = 0, j = 0, count = 0;

    while (i < n1 && j < n2) {
        if (arr1[i] < arr2[j]) {
            count++;
            if (count == k) return arr1[i];
            i++;
        } else {
            count++;
            if (count == k) return arr2[j];
            j++;
        }
    }

    // If elements left in arr1
    while (i < n1) {
        count++;
        if (count == k) return arr1[i];
        i++;
    }

    // If elements left in arr2
    while (j < n2) {
        count++;
        if (count == k) return arr2[j];
        j++;
    }

    return -1; // if k is larger than total elements
}

int main() {
    int arr1[] = {2, 3, 6, 7, 9};
    int arr2[] = {1, 4, 8, 10};
    int n1 = sizeof(arr1) / sizeof(arr1[0]);
    int n2 = sizeof(arr2) / sizeof(arr2[0]);
    int k = 5;

    int result = findKthSmallest(arr1, n1, arr2, n2, k);

    if (result != -1)
        printf("%d-th smallest element is %d\n", k, result);
    else
        printf("Invalid k (larger than total elements)\n");

    return 0;
}


```

## Sample Output:

```c

5-th smallest element is 6

```
