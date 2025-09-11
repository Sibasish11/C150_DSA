# Develop a program to find pairs with a given sum in an array using a hash set.

```c

#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

#define TABLE_SIZE 1000 

// Simple hash set implementation for integers
typedef struct Node {
    int key;
    struct Node* next;
} Node;

Node* hashTable[TABLE_SIZE];

int hashFunction(int key) {
    if (key < 0) key = -key;
    return key % TABLE_SIZE;
}

// Insert into hash set
void insert(int key) {
    int hashIndex = hashFunction(key);
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->key = key;
    newNode->next = hashTable[hashIndex];
    hashTable[hashIndex] = newNode;
}

// Search in hash set
bool search(int key) {
    int hashIndex = hashFunction(key);
    Node* temp = hashTable[hashIndex];
    while (temp) {
        if (temp->key == key)
            return true;
        temp = temp->next;
    }
    return false;
}

// Free hash table memory
void freeTable() {
    for (int i = 0; i < TABLE_SIZE; i++) {
        Node* temp = hashTable[i];
        while (temp) {
            Node* toDelete = temp;
            temp = temp->next;
            free(toDelete);
        }
        hashTable[i] = NULL;
    }
}

// Function to find pairs with given sum
void findPairs(int arr[], int n, int target) {
    printf("Pairs with sum %d:\n", target);
    for (int i = 0; i < n; i++) {
        int complement = target - arr[i];
        if (search(complement)) {
            printf("(%d, %d)\n", complement, arr[i]);
        }
        insert(arr[i]);
    }
}

int main() {
    int arr[] = {8, 7, 2, 5, 3, 1};
    int n = sizeof(arr) / sizeof(arr[0]);
    int target = 10;

    findPairs(arr, n, target);

    freeTable();
    return 0;
}


```

## Example Output:

```c

Pairs with sum 10:
(2, 8)
(3, 7)

```
