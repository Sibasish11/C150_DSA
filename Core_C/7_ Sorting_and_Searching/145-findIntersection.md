# Develop a program to find the intersection of two sorted arrays.

```c

#include <stdio.h>

// Function to print intersection of two sorted arrays
void findIntersection(int arr1[], int n1, int arr2[], int n2) {
    int i = 0, j = 0;

    printf("Intersection: ");
    while (i < n1 && j < n2) {
        if (arr1[i] == arr2[j]) {
            printf("%d ", arr1[i]);
            i++;
            j++;
        }
        else if (arr1[i] < arr2[j]) {
            i++;
        }
        else {
            j++;
        }
    }
    printf("\n");
}

int main() {
    int arr1[] = {1, 2, 4, 5, 6};
    int arr2[] = {2, 4, 6, 8};
    int n1 = sizeof(arr1) / sizeof(arr1[0]);
    int n2 = sizeof(arr2) / sizeof(arr2[0]);

    findIntersection(arr1, n1, arr2, n2);

    return 0;
}


```

## Sample Output:

```c

Intersection: 2 4 6 

```
