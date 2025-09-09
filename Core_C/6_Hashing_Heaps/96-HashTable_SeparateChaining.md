# Implement a Hash Table with separate chaining (using linked lists) for collision handling. Include insert, search, and delete operations.

```c

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define TABLE_SIZE 10

// Node for linked list (chaining)
struct Node {
    int key;
    struct Node* next;
};

// Hash table array (each index points to a linked list)
struct Node* hashTable[TABLE_SIZE];

// Hash Function
int hash(int key) {
    return key % TABLE_SIZE;
}

// Insert key into hash table
void insert(int key) {
    int index = hash(key);
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->key = key;
    newNode->next = hashTable[index]; // Insert at beginning
    hashTable[index] = newNode;
    printf("Inserted %d at index %d\n", key, index);
}

// Search key in hash table
int search(int key) {
    int index = hash(key);
    struct Node* temp = hashTable[index];
    while (temp) {
        if (temp->key == key) return 1;
        temp = temp->next;
    }
    return 0;
}

// Delete key from hash table
void deleteKey(int key) {
    int index = hash(key);
    struct Node* temp = hashTable[index];
    struct Node* prev = NULL;

    while (temp) {
        if (temp->key == key) {
            if (prev) prev->next = temp->next;
            else hashTable[index] = temp->next;
            free(temp);
            printf("Deleted %d from index %d\n", key, index);
            return;
        }
        prev = temp;
        temp = temp->next;
    }
    printf("Key %d not found\n", key);
}

// Print hash table
void printTable() {
    for (int i = 0; i < TABLE_SIZE; i++) {
        printf("Index %d: ", i);
        struct Node* temp = hashTable[i];
        while (temp) {
            printf("%d -> ", temp->key);
            temp = temp->next;
        }
        printf("NULL\n");
    }
}

int main() {
    // Initialize hash table
    for (int i = 0; i < TABLE_SIZE; i++) hashTable[i] = NULL;

    insert(15);
    insert(25);
    insert(35);
    insert(20);

    printTable();

    printf("\nSearch 25: %s\n", search(25) ? "Found" : "Not Found");
    printf("Search 40: %s\n", search(40) ? "Found" : "Not Found");

    deleteKey(25);
    deleteKey(40);

    printTable();

    return 0;
}

```

## Example Run:

- Input/Operations inside main:

```c

insert(15);
insert(25);
insert(35);
insert(20);
search(25);
search(40);
deleteKey(25);
deleteKey(40);

```

- Output:

```c

Inserted 15 at index 5
Inserted 25 at index 5
Inserted 35 at index 5
Inserted 20 at index 0

Index 0: 20 -> NULL
Index 1: NULL
Index 2: NULL
Index 3: NULL
Index 4: NULL
Index 5: 35 -> 25 -> 15 -> NULL
Index 6: NULL
Index 7: NULL
Index 8: NULL
Index 9: NULL

Search 25: Found
Search 40: Not Found
Deleted 25 from index 5
Key 40 not found

Index 0: 20 -> NULL
Index 1: NULL
Index 2: NULL
Index 3: NULL
Index 4: NULL
Index 5: 35 -> 15 -> NULL
Index 6: NULL
Index 7: NULL
Index 8: NULL
Index 9: NULL

```
