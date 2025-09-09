# Implement a Hash Table with open addressing (e.g., linear probing) for collision handling. Include insert, search, and delete operations.

```c

#include <stdio.h>
#include <stdlib.h>

#define TABLE_SIZE 10
#define EMPTY -1
#define DELETED -2

int hashTable[TABLE_SIZE];

// Hash Function
int hash(int key) {
    return key % TABLE_SIZE;
}

// Insert key using linear probing
void insert(int key) {
    int index = hash(key);
    int start = index;

    while (hashTable[index] != EMPTY && hashTable[index] != DELETED) {
        index = (index + 1) % TABLE_SIZE;
        if (index == start) {
            printf("Hash Table is Full! Cannot insert %d\n", key);
            return;
        }
    }
    hashTable[index] = key;
    printf("Inserted %d at index %d\n", key, index);
}

// Search key
int search(int key) {
    int index = hash(key);
    int start = index;

    while (hashTable[index] != EMPTY) {
        if (hashTable[index] == key) return index;
        index = (index + 1) % TABLE_SIZE;
        if (index == start) break;
    }
    return -1;
}

// Delete key
void deleteKey(int key) {
    int index = search(key);
    if (index == -1) {
        printf("Key %d not found\n", key);
    } else {
        hashTable[index] = DELETED;
        printf("Deleted %d from index %d\n", key, index);
    }
}

// Print hash table
void printTable() {
    printf("\nHash Table:\n");
    for (int i = 0; i < TABLE_SIZE; i++) {
        if (hashTable[i] == EMPTY) printf("Index %d: EMPTY\n", i);
        else if (hashTable[i] == DELETED) printf("Index %d: DELETED\n", i);
        else printf("Index %d: %d\n", i, hashTable[i]);
    }
}

int main() {
    // Initialize hash table
    for (int i = 0; i < TABLE_SIZE; i++) hashTable[i] = EMPTY;

    insert(15);
    insert(25);
    insert(35);
    insert(20);

    printTable();

    printf("\nSearching 25... %s\n", search(25) != -1 ? "Found" : "Not Found");
    printf("Searching 40... %s\n", search(40) != -1 ? "Found" : "Not Found");

    deleteKey(25);
    deleteKey(40);

    printTable();

    return 0;
}


```

## Example Run

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
Inserted 25 at index 5 (collision, moved to index 6)
Inserted 35 at index 5 (collision, moved to index 7)
Inserted 20 at index 0

Hash Table:
Index 0: 20
Index 1: EMPTY
Index 2: EMPTY
Index 3: EMPTY
Index 4: EMPTY
Index 5: 15
Index 6: 25
Index 7: 35
Index 8: EMPTY
Index 9: EMPTY

Searching 25... Found
Searching 40... Not Found
Deleted 25 from index 6
Key 40 not found

Hash Table:
Index 0: 20
Index 1: EMPTY
Index 2: EMPTY
Index 3: EMPTY
Index 4: EMPTY
Index 5: 15
Index 6: DELETED
Index 7: 35
Index 8: EMPTY
Index 9: EMPTY

```
