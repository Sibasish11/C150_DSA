# Implement a program to perform a min-heap from a given array.

```c

#include <stdio.h>

void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Heapify a subtree rooted at index i
void heapify(int arr[], int n, int i) {
    int smallest = i;       // Assume root is smallest
    int left = 2 * i + 1;   // Left child index
    int right = 2 * i + 2;  // Right child index

    // If left child is smaller than root
    if (left < n && arr[left] < arr[smallest])
        smallest = left;

    // If right child is smaller than smallest so far
    if (right < n && arr[right] < arr[smallest])
        smallest = right;

    // If smallest is not root, swap and continue heapify
    if (smallest != i) {
        swap(&arr[i], &arr[smallest]);
        heapify(arr, n, smallest);
    }
}

// Function to build a Min-Heap
void buildMinHeap(int arr[], int n) {
    // Start from last non-leaf node and heapify each
    for (int i = n / 2 - 1; i >= 0; i--) {
        heapify(arr, n, i);
    }
}

// Function to print array
void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int main() {
    int arr[] = {5, 3, 8, 4, 1, 2};
    int n = sizeof(arr) / sizeof(arr[0]);

    printf("Original array:\n");
    printArray(arr, n);

    buildMinHeap(arr, n);

    printf("Array represented as Min-Heap:\n");
    printArray(arr, n);

    return 0;
}


```

## Example Output:

```c

Original array:
5 3 8 4 1 2 
Array represented as Min-Heap:
1 3 2 4 5 8 

```
