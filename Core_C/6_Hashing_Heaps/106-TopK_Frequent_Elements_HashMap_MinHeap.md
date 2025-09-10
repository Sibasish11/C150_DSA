# Implement a program to find the top K most frequent elements in an array using a Hash Map and a Min-Heap.

```c

#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

#define MAX 1000 

// Structure for heap node
typedef struct {
    int element;
    int freq;
} HeapNode;

// Min-Heap functions
void swap(HeapNode *a, HeapNode *b) {
    HeapNode temp = *a;
    *a = *b;
    *b = temp;
}

void heapify(HeapNode heap[], int n, int i) {
    int smallest = i;
    int left = 2*i + 1, right = 2*i + 2;

    if (left < n && heap[left].freq < heap[smallest].freq)
        smallest = left;
    if (right < n && heap[right].freq < heap[smallest].freq)
        smallest = right;

    if (smallest != i) {
        swap(&heap[i], &heap[smallest]);
        heapify(heap, n, smallest);
    }
}

void buildMinHeap(HeapNode heap[], int n) {
    for (int i = n/2 - 1; i >= 0; i--)
        heapify(heap, n, i);
}

// Insert into Min-Heap
void insertHeap(HeapNode heap[], int *n, HeapNode node, int k) {
    if (*n < k) {
        heap[*n] = node;
        (*n)++;
        buildMinHeap(heap, *n);
    } else if (node.freq > heap[0].freq) {
        heap[0] = node;
        heapify(heap, *n, 0);
    }
}

// Find top K frequent elements
void topKFrequent(int arr[], int n, int k) {
    // Step 1: Count frequencies
    int freq[MAX] = {0};
    for (int i = 0; i < n; i++)
        freq[arr[i]]++;

    // Step 2: Use Min-Heap
    HeapNode heap[k];
    int heapSize = 0;

    for (int i = 0; i < MAX; i++) {
        if (freq[i] > 0) {
            HeapNode node = {i, freq[i]};
            insertHeap(heap, &heapSize, node, k);
        }
    }

    // Step 3: Print result
    printf("Top %d frequent elements: ", k);
    for (int i = 0; i < heapSize; i++)
        printf("%d ", heap[i].element);
    printf("\n");
}

int main() {
    int arr[] = {1, 1, 1, 2, 2, 3, 3, 3, 3, 4};
    int n = sizeof(arr)/sizeof(arr[0]);
    int k = 2;

    topKFrequent(arr, n, k);

    return 0;
}


```

## Example Run

- Input:

```c

arr = [1, 1, 1, 2, 2, 3, 3, 3, 3, 4]
k = 2

```

- Output:

```c

Top 2 frequent elements: 1 3

```
