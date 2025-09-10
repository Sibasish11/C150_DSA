# Write a program to merge K sorted lists/arrays into a single sorted list using a Min-Heap.

```c

#include <stdio.h>
#include <stdlib.h>

// Structure for heap node
typedef struct {
    int value;   // element value
    int arrIdx;  // which array
    int eleIdx;  // index inside that array
} HeapNode;

// Swap two heap nodes
void swap(HeapNode *a, HeapNode *b) {
    HeapNode temp = *a;
    *a = *b;
    *b = temp;
}

// Min-Heapify function
void heapify(HeapNode heap[], int n, int i) {
    int smallest = i;
    int left = 2*i + 1, right = 2*i + 2;

    if (left < n && heap[left].value < heap[smallest].value)
        smallest = left;
    if (right < n && heap[right].value < heap[smallest].value)
        smallest = right;

    if (smallest != i) {
        swap(&heap[i], &heap[smallest]);
        heapify(heap, n, smallest);
    }
}

// Build Min-Heap
void buildMinHeap(HeapNode heap[], int n) {
    for (int i = n/2 - 1; i >= 0; i--)
        heapify(heap, n, i);
}

// Function to merge K sorted arrays
void mergeKSortedArrays(int arr[][100], int sizes[], int k) {
    HeapNode heap[k];
    int totalSize = 0;

    // Insert first element of each array into heap
    for (int i = 0; i < k; i++) {
        heap[i].value = arr[i][0];
        heap[i].arrIdx = i;
        heap[i].eleIdx = 0;
        totalSize += sizes[i];
    }

    buildMinHeap(heap, k);

    printf("Merged Sorted Array: ");

    // Extract elements from heap
    for (int count = 0; count < totalSize; count++) {
        HeapNode root = heap[0];
        printf("%d ", root.value);

        // Replace root with next element of same array
        if (root.eleIdx + 1 < sizes[root.arrIdx]) {
            heap[0].value = arr[root.arrIdx][root.eleIdx + 1];
            heap[0].eleIdx += 1;
        } else {
            heap[0].value = __INT_MAX__; // No more elements, set to infinity
        }

        heapify(heap, k, 0);
    }
    printf("\n");
}

int main() {
    int k = 3;
    int arr[3][100] = {
        {1, 4, 7},
        {2, 5, 8},
        {3, 6, 9}
    };
    int sizes[] = {3, 3, 3};

    mergeKSortedArrays(arr, sizes, k);

    return 0;
}


```

## Example Run

- Input:

```c

Arrays:
[1, 4, 7]
[2, 5, 8]
[3, 6, 9]

```

- Output:

```c

Merged Sorted Array: 1 2 3 4 5 6 7 8 9

```
