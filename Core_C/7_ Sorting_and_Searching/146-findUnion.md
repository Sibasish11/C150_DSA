# Write a program to find the union of two sorted arrays.

```c

#include <stdio.h>

// Function to print union of two sorted arrays
void findUnion(int arr1[], int n1, int arr2[], int n2) {
    int i = 0, j = 0;

    printf("Union: ");
    while (i < n1 && j < n2) {
        if (arr1[i] < arr2[j]) {
            printf("%d ", arr1[i]);
            i++;
        }
        else if (arr1[i] > arr2[j]) {
            printf("%d ", arr2[j]);
            j++;
        }
        else { // equal elements, print once
            printf("%d ", arr1[i]);
            i++;
            j++;
        }
    }

    // Print remaining elements
    while (i < n1) {
        printf("%d ", arr1[i]);
        i++;
    }
    while (j < n2) {
        printf("%d ", arr2[j]);
        j++;
    }

    printf("\n");
}

int main() {
    int arr1[] = {1, 2, 4, 5, 6};
    int arr2[] = {2, 3, 5, 7};
    int n1 = sizeof(arr1) / sizeof(arr1[0]);
    int n2 = sizeof(arr2) / sizeof(arr2[0]);

    findUnion(arr1, n1, arr2, n2);

    return 0;
}


```

## Sample Output:

```c

Union: 1 2 3 4 5 6 7 

```
