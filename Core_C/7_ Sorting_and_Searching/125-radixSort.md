# Write a program to implement Radix Sort to sort an array of non-negative integers.

```c

#include <stdio.h>

// Function to get the maximum value in arr[]
int getMax(int arr[], int n) {
    int max = arr[0];
    for (int i = 1; i < n; i++)
        if (arr[i] > max)
            max = arr[i];
    return max;
}

// A function to perform Counting Sort based on a specific digit
void countingSort(int arr[], int n, int exp) {
    int output[n];  // output array
    int count[10] = {0}; // digits 0-9

    // Count occurrences of digits
    for (int i = 0; i < n; i++)
        count[(arr[i] / exp) % 10]++;

    // Update count[i] to contain actual position in output[]
    for (int i = 1; i < 10; i++)
        count[i] += count[i - 1];

    // Build the output array (stable sort: process from right to left)
    for (int i = n - 1; i >= 0; i--) {
        output[count[(arr[i] / exp) % 10] - 1] = arr[i];
        count[(arr[i] / exp) % 10]--;
    }

    // Copy output[] back to arr[]
    for (int i = 0; i < n; i++)
        arr[i] = output[i];
}

// The main Radix Sort function
void radixSort(int arr[], int n) {
    int m = getMax(arr, n); // find maximum number

    // Apply Counting Sort to each digit (exp = 1, 10, 100, ...)
    for (int exp = 1; m / exp > 0; exp *= 10)
        countingSort(arr, n, exp);
}

// Function to print array
void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++)
        printf("%d ", arr[i]);
    printf("\n");
}

int main() {
    int arr[] = {170, 45, 75, 90, 802, 24, 2, 66};
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("Unsorted array: ");
    printArray(arr, n);

    radixSort(arr, n);

    printf("Sorted array: ");
    printArray(arr, n);

    return 0;
}


```

## Output:

```c

Unsorted array: 170 45 75 90 802 24 2 66
Sorted array: 2 24 45 66 75 90 170 802

```


