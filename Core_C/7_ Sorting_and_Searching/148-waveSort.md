# Develop a program to sort an array in wave form (e.g., arr[0] >= arr[1] <= arr[2] >= arr[3] ...).

```c

#include <stdio.h>

// Function to swap two numbers
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Function to sort array in wave form
void waveSort(int arr[], int n) {
    for (int i = 0; i < n; i += 2) {
        // If current even index element is smaller than previous
        if (i > 0 && arr[i] < arr[i - 1]) {
            swap(&arr[i], &arr[i - 1]);
        }
        // If current even index element is smaller than next
        if (i < n - 1 && arr[i] < arr[i + 1]) {
            swap(&arr[i], &arr[i + 1]);
        }
    }
}

int main() {
    int arr[] = {10, 90, 49, 2, 1, 5, 23};
    int n = sizeof(arr) / sizeof(arr[0]);

    waveSort(arr, n);

    printf("Array in wave form: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    return 0;
}

```

## Sample Input:

```c

arr = [10, 90, 49, 2, 1, 5, 23]

```

 ## Sample Output:

 ```
 
Array in wave form: 90 10 49 1 5 2 23

```
