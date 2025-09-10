# Implement a program to implement a Max-Heap data structure. Include insert, deleteMax, peekMax, and heapify operations.

```c

#include <stdio.h>
#include <stdlib.h>

#define MAX_SIZE 100

struct MaxHeap {
    int arr[MAX_SIZE];
    int size;
};

// Swap two integers
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Heapify (max-heapify) at index i
void heapify(struct MaxHeap *heap, int i) {
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;

    if (left < heap->size && heap->arr[left] > heap->arr[largest])
        largest = left;

    if (right < heap->size && heap->arr[right] > heap->arr[largest])
        largest = right;

    if (largest != i) {
        swap(&heap->arr[i], &heap->arr[largest]);
        heapify(heap, largest);
    }
}

// Insert element into Max-Heap
void insert(struct MaxHeap *heap, int value) {
    if (heap->size == MAX_SIZE) {
        printf("Heap Overflow!\n");
        return;
    }

    // Insert at end
    int i = heap->size++;
    heap->arr[i] = value;

    // Bubble up
    while (i != 0 && heap->arr[(i - 1) / 2] < heap->arr[i]) {
        swap(&heap->arr[i], &heap->arr[(i - 1) / 2]);
        i = (i - 1) / 2;
    }
}

// Return max element
int peekMax(struct MaxHeap *heap) {
    if (heap->size <= 0) {
        printf("Heap is empty!\n");
        return -1;
    }
    return heap->arr[0];
}

// Delete max element
int deleteMax(struct MaxHeap *heap) {
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
void printHeap(struct MaxHeap *heap) {
    printf("Heap elements: ");
    for (int i = 0; i < heap->size; i++)
        printf("%d ", heap->arr[i]);
    printf("\n");
}

int main() {
    struct MaxHeap heap;
    heap.size = 0;

    insert(&heap, 10);
    insert(&heap, 20);
    insert(&heap, 5);
    insert(&heap, 30);
    insert(&heap, 2);

    printHeap(&heap);

    printf("Max element: %d\n", peekMax(&heap));

    printf("Deleted Max: %d\n", deleteMax(&heap));
    printHeap(&heap);

    printf("Deleted Max: %d\n", deleteMax(&heap));
    printHeap(&heap);

    return 0;
}


```

## Example Run:

- Input / Operations:

```c

Insert: 10, 20, 5, 30, 40
Peek Max
Delete Max
Delete Max

```

- Output:

```c

Heap elements: 40 30 5 10 20 
Max element: 40
Deleted Max: 40
Heap elements: 30 20 5 10 
Deleted Max: 30
Heap elements: 20 10 5

```
