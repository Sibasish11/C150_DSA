# Develop a program to find whether an array contains duplicate elements within a window of size k using a Hash Set.

```c

#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

// Simple Hash Set implementation using array & linear probing
#define TABLE_SIZE 10007  // prime number for hash table

typedef struct Node {
    int key;
    struct Node* next;
} Node;

typedef struct {
    Node* table[TABLE_SIZE];
} HashSet;

// Hash function
int hash(int key) {
    if (key < 0) key = -key;
    return key % TABLE_SIZE;
}

// Initialize HashSet
HashSet* createSet() {
    HashSet* set = (HashSet*)malloc(sizeof(HashSet));
    for (int i = 0; i < TABLE_SIZE; i++)
        set->table[i] = NULL;
    return set;
}

// Insert key
void insert(HashSet* set, int key) {
    int h = hash(key);
    Node* node = set->table[h];
    while (node) {
        if (node->key == key) return; // already exists
        node = node->next;
    }
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->key = key;
    newNode->next = set->table[h];
    set->table[h] = newNode;
}

// Search key
bool contains(HashSet* set, int key) {
    int h = hash(key);
    Node* node = set->table[h];
    while (node) {
        if (node->key == key) return true;
        node = node->next;
    }
    return false;
}

// Remove key
void removeKey(HashSet* set, int key) {
    int h = hash(key);
    Node* node = set->table[h], *prev = NULL;
    while (node) {
        if (node->key == key) {
            if (prev) prev->next = node->next;
            else set->table[h] = node->next;
            free(node);
            return;
        }
        prev = node;
        node = node->next;
    }
}

// Free memory
void freeSet(HashSet* set) {
    for (int i = 0; i < TABLE_SIZE; i++) {
        Node* node = set->table[i];
        while (node) {
            Node* temp = node;
            node = node->next;
            free(temp);
        }
    }
    free(set);
}

// Main function to check duplicates within k
bool containsNearbyDuplicate(int arr[], int n, int k) {
    HashSet* set = createSet();

    for (int i = 0; i < n; i++) {
        if (contains(set, arr[i])) {
            freeSet(set);
            return true;
        }

        insert(set, arr[i]);

        // Maintain sliding window size = k
        if (i >= k) {
            removeKey(set, arr[i - k]);
        }
    }

    freeSet(set);
    return false;
}

int main() {
    int arr[] = {1, 2, 3, 1, 4, 5};
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 3;

    if (containsNearbyDuplicate(arr, n, k))
        printf("Duplicate found within distance %d\n", k);
    else
        printf("No duplicate found within distance %d\n", k);

    return 0;
}


```

## Example Run:

- Input:

```c

arr = [1, 2, 3, 1, 4, 5], k = 3

```

- Output:

```c

Duplicate found within distance 3

```
