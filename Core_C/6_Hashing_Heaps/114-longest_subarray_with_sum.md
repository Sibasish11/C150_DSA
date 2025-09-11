# Write a program to find the longest subarray with a given sum using a hash map.

```c

#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

#define TABLE_SIZE 1000  // Hash table size for prefix sums

// HashMap Node (prefixSum -> firstIndex)
typedef struct Node {
    int key;   // prefix sum
    int value; // index
    struct Node* next;
} Node;

Node* hashTable[TABLE_SIZE];

// Hash function
int hashFunction(int key) {
    if (key < 0) key = -key;
    return key % TABLE_SIZE;
}

// Insert into hash map if not present
void insert(int key, int value) {
    int hashIndex = hashFunction(key);
    Node* temp = hashTable[hashIndex];

    while (temp) {
        if (temp->key == key) return; // already present
        temp = temp->next;
    }

    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->key = key;
    newNode->value = value;
    newNode->next = hashTable[hashIndex];
    hashTable[hashIndex] = newNode;
}

// Search in hash map
int search(int key, int* found) {
    int hashIndex = hashFunction(key);
    Node* temp = hashTable[hashIndex];
    while (temp) {
        if (temp->key == key) {
            *found = 1;
            return temp->value;
        }
        temp = temp->next;
    }
    *found = 0;
    return -1;
}

// Free memory
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

// Function to find longest subarray with given sum
int longestSubarrayWithSum(int arr[], int n, int target) {
    int prefixSum = 0;
    int maxLen = 0;

    for (int i = 0; i < n; i++) {
        prefixSum += arr[i];

        // Case 1: Subarray from index 0 to i
        if (prefixSum == target) {
            if (i + 1 > maxLen) maxLen = i + 1;
        }

        // Case 2: Check if prefixSum - target was seen before
        int found;
        int index = search(prefixSum - target, &found);
        if (found) {
            if (i - index > maxLen) maxLen = i - index;
        }

        // Insert prefixSum only if not already present
        insert(prefixSum, i);
    }

    return maxLen;
}

int main() {
    int arr[] = {1, 2, 3, 0, 3, -3, 2, 1};
    int n = sizeof(arr) / sizeof(arr[0]);
    int target = 3;

    int result = longestSubarrayWithSum(arr, n, target);
    printf("Length of the longest subarray with sum %d = %d\n", target, result);

    freeTable();
    return 0;
}


```

## Example Output:

```c

Length of the longest subarray with sum 3 = 5

```

- (Here the subarray [3, 0, 3, -3, 2] has sum 3 and length 5.)
