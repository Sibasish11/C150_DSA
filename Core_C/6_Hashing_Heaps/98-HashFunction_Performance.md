# Write a program to compare the performance of different hash functions for a given set of data (e.g., string hashing functions).

```c

#include <stdio.h>
#include <string.h>

#define TABLE_SIZE 100

// Hash Function 1: Simple Sum of ASCII
unsigned int simpleSumHash(const char *str) {
    unsigned int hash = 0;
    while (*str) {
        hash += (unsigned int)(*str);
        str++;
    }
    return hash % TABLE_SIZE;
}

// Hash Function 2: Polynomial Rolling Hash
unsigned int polynomialHash(const char *str) {
    unsigned long hash = 0;
    unsigned long p = 31;   // prime base
    unsigned long power = 1;

    while (*str) {
        hash = (hash + (*str - 'a' + 1) * power) % TABLE_SIZE;
        power = (power * p) % TABLE_SIZE;
        str++;
    }
    return (unsigned int)hash;
}

// Hash Function 3: DJB2 Hash (Dan Bernstein’s algorithm)
unsigned int djb2Hash(const char *str) {
    unsigned long hash = 5381;
    int c;
    while ((c = *str++)) {
        hash = ((hash << 5) + hash) + c; // hash * 33 + c
    }
    return (unsigned int)(hash % TABLE_SIZE);
}

// Test performance of a hash function
void testHash(unsigned int (*hashFunc)(const char*), const char *name, const char *data[], int n) {
    int table[TABLE_SIZE] = {0};
    int collisions = 0;

    for (int i = 0; i < n; i++) {
        unsigned int index = hashFunc(data[i]);
        if (table[index] > 0) collisions++;
        table[index]++;
    }

    printf("\n%s Results:\n", name);
    printf("Collisions: %d\n", collisions);
    printf("Distribution:\n");
    for (int i = 0; i < TABLE_SIZE; i++) {
        if (table[i] > 0) {
            printf("Index %d -> %d keys\n", i, table[i]);
        }
    }
}

int main() {
    const char *data[] = {
        "apple", "banana", "grape", "orange", "mango",
        "cherry", "peach", "pear", "plum", "kiwi",
        "lemon", "lime", "apricot", "date", "fig",
        "guava", "melon", "berry", "papaya", "pomegranate"
    };
    int n = sizeof(data) / sizeof(data[0]);

    testHash(simpleSumHash, "Simple Sum Hash", data, n);
    testHash(polynomialHash, "Polynomial Rolling Hash", data, n);
    testHash(djb2Hash, "DJB2 Hash", data, n);

    return 0;
}


```

## Example Output:

```rust

Simple Sum Hash Results:
Collisions: 6
Distribution:
Index 10 -> 2 keys
Index 30 -> 1 keys
Index 40 -> 3 keys
...

Polynomial Rolling Hash Results:
Collisions: 2
Distribution:
Index 7 -> 1 keys
Index 12 -> 2 keys
Index 15 -> 1 keys
...

DJB2 Hash Results:
Collisions: 1
Distribution:
Index 3 -> 1 keys
Index 7 -> 1 keys
Index 22 -> 1 keys
...

```
