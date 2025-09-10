# Develop a program to find the Kth smallest element in an array using a Min-Heap.

```c

#include <stdio.h>

// Swap
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Heapify function for Min-Heap
void heapify(int arr[], int n, int i) {
    int smallest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < n && arr[left] < arr[smallest])
        smallest = left;

    if (right < n && arr[right] < arr[smallest])
        smallest = right;

    if (smallest != i) {
        swap(&arr[i], &arr[smallest]);
        heapify(arr, n, smallest);
    }
}

// Build Min-Heap
void buildMinHeap(int arr[], int n) {
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i);
}

// Extract minimum element from heap
int extractMin(int arr[], int *n) {
    if (*n <= 0)
        return -1;

    int root = arr[0];
    arr[0] = arr[--(*n)];
    heapify(arr, *n, 0);

    return root;
}

// Find Kth smallest element
int kthSmallest(int arr[], int n, int k) {
    buildMinHeap(arr, n);

    for (int i = 1; i < k; i++)
        extractMin(arr, &n);

    return extractMin(arr, &n);
}

int main() {
    int arr[] = {12, 3, 5, 7, 19, 1};
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    int result = kthSmallest(arr, n, k);
    printf("%dth smallest element is %d\n", k, result);

    return 0;
}


```


## 🎯 Example Run

- Input:

```c

Array: 12 3 5 7 19 1
K = 3

```

- Output:

```c

3th smallest element is 5

```
