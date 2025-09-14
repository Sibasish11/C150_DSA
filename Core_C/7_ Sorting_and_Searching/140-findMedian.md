# Write a program to find the median of two sorted arrays of different sizes.

```c

#include <stdio.h>

double findMedian(int arr1[], int n1, int arr2[], int n2) {
    int merged[n1 + n2];
    int i = 0, j = 0, k = 0;

    // Merge the two arrays
    while (i < n1 && j < n2) {
        if (arr1[i] < arr2[j])
            merged[k++] = arr1[i++];
        else
            merged[k++] = arr2[j++];
    }
    while (i < n1) merged[k++] = arr1[i++];
    while (j < n2) merged[k++] = arr2[j++];

    int total = n1 + n2;

    // If odd length, return middle element
    if (total % 2 == 1) {
        return merged[total / 2];
    }
    // If even length, return average of middle two
    else {
        return (merged[(total - 1) / 2] + merged[total / 2]) / 2.0;
    }
}

// Driver program
int main() {
    int arr1[] = {1, 3, 5};
    int arr2[] = {2, 4, 6, 8};
    int n1 = sizeof(arr1) / sizeof(arr1[0]);
    int n2 = sizeof(arr2) / sizeof(arr2[0]);

    double median = findMedian(arr1, n1, arr2, n2);
    printf("Median = %.2f\n", median);

    return 0;
}


```

## Sample Output:

```c

Median = 4.00

```
