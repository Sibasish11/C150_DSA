# Write a program to implement a Min-Heap data structure. Include insert, deleteMin, peekMin, and heapify operations.

```c

#include <stdio.h>
#include <stdlib.h>

#define MAX_SIZE 100

struct MinHeap {
    int arr[MAX_SIZE];
    int size;
};

// Swap two integers
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Heapify (min-heapify) at index i
void heapify(struct MinHeap *heap, int i) {
    int smallest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < heap->size && heap->arr[left] < heap->arr[smallest])
        smallest = left;

    if (right < heap->size && heap->arr[right] < heap->arr[smallest])
        smallest = right;

    if (smallest != i) {
        swap(&heap->arr[i], &heap->arr[smallest]);
        heapify(heap, smallest);
    }
}

// Insert element into Min-Heap
void insert(struct MinHeap *heap, int value) {
    if (heap->size == MAX_SIZE) {
        printf("Heap Overflow!\n");
        return;
    }

    // Insert at end
    int i = heap->size++;
    heap->arr[i] = value;

    // Bubble up
    while (i != 0 && heap->arr[(i - 1) / 2] > heap->arr[i]) {
        swap(&heap->arr[i], &heap->arr[(i - 1) / 2]);
        i = (i - 1) / 2;
    }
}

// Return min element
int peekMin(struct MinHeap *heap) {
    if (heap->size <= 0) {
        printf("Heap is empty!\n");
        return -1;
    }
    return heap->arr[0];
}

// Delete min element
int deleteMin(struct MinHeap *heap) {
    if (heap->size <= 0) {
        printf("Heap Underflow!\n");
        return -1;
    }
    if (heap->size == 1)
        return heap->arr[--heap->size];

    int root = heap->arr[0];
    heap->arr[0] = heap->arr[--heap->size];
    heapify(heap, 0);
    return root;
}

// Print heap
void printHeap(struct MinHeap *heap) {
    printf("Heap elements: ");
    for (int i = 0; i < heap->size; i++)
        printf("%d ", heap->arr[i]);
    printf("\n");
}

int main() {
    struct MinHeap heap;
    heap.size = 0;

    insert(&heap, 10);
    insert(&heap, 20);
    insert(&heap, 5);
    insert(&heap, 30);
    insert(&heap, 2);

    printHeap(&heap);

    printf("Min element: %d\n", peekMin(&heap));

    printf("Deleted Min: %d\n", deleteMin(&heap));
    printHeap(&heap);

    printf("Deleted Min: %d\n", deleteMin(&heap));
    printHeap(&heap);

    return 0;
}

```

## Example Run:

- Input / Operations:

```c

Insert: 10, 20, 5, 30, 2
Peek Min
Delete Min
Delete Min

```

- Output:

```c

Heap elements: 2 10 5 30 20 
Min element: 2
Deleted Min: 2
Heap elements: 5 10 20 30 
Deleted Min: 5
Heap elements: 10 30 20

```
