# Develop a program to count the frequency of each element in an array using a Hash Map.

```c

#include <stdio.h>
#include <stdlib.h>

#define SIZE 10  // Hash Table size

// Node structure for linked list (separate chaining)
struct Node {
    int key;
    int count;
    struct Node* next;
};

int hash(int key) {
    return key % SIZE;
}

void insert(struct Node* table[], int key) {
    int index = hash(key);
    struct Node* head = table[index];
    
    // Search if key already exists
    struct Node* temp = head;
    while (temp != NULL) {
        if (temp->key == key) {
            temp->count++;
            return;
        }
        temp = temp->next;
    }
    
    // If key not found, insert new node
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->key = key;
    newNode->count = 1;
    newNode->next = head;
    table[index] = newNode;
}

// Print all frequencies
void printFrequencies(struct Node* table[]) {
    for (int i = 0; i < SIZE; i++) {
        struct Node* temp = table[i];
        while (temp != NULL) {
            printf("%d -> %d\n", temp->key, temp->count);
            temp = temp->next;
        }
    }
}

int main() {
    int arr[] = {10, 20, 10, 30, 20, 40, 10, 30, 50, 20};
    int n = sizeof(arr) / sizeof(arr[0]);

    // Initialize hash table
    struct Node* hashTable[SIZE] = {NULL};

    // Insert elements into hash table
    for (int i = 0; i < n; i++) {
        insert(hashTable, arr[i]);
    }

    printf("Frequencies of elements:\n");
    printFrequencies(hashTable);

    return 0;
}


```

## Example Output:

```rust

Frequencies of elements:
10 -> 3
20 -> 3
30 -> 2
40 -> 1
50 -> 1

```
