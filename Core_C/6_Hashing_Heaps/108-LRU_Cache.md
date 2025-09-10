# Write a program to implement a simple "least recently used" (LRU) cache using a Hash Map and a Doubly Linked List.

```c

#include <stdio.h>
#include <stdlib.h>

#define HASH_SIZE 1000  // Hash map size

// Doubly Linked List Node
typedef struct Node {
    int key, value;
    struct Node* prev;
    struct Node* next;
} Node;

// Hash Map entry
typedef struct {
    Node* node;
} HashEntry;

// LRU Cache structure
typedef struct {
    int capacity;
    int size;
    HashEntry* map;
    Node* head;
    Node* tail;
} LRUCache;

// Utility: Create new node
Node* createNode(int key, int value) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    newNode->key = key;
    newNode->value = value;
    newNode->prev = newNode->next = NULL;
    return newNode;
}

// Utility: Hash function
int hash(int key) {
    return key % HASH_SIZE;
}

// Initialize cache
LRUCache* lRUCacheCreate(int capacity) {
    LRUCache* cache = (LRUCache*)malloc(sizeof(LRUCache));
    cache->capacity = capacity;
    cache->size = 0;
    cache->map = (HashEntry*)calloc(HASH_SIZE, sizeof(HashEntry));

    // Dummy head & tail
    cache->head = createNode(0, 0);
    cache->tail = createNode(0, 0);
    cache->head->next = cache->tail;
    cache->tail->prev = cache->head;

    return cache;
}

// Remove a node from linked list
void removeNode(Node* node) {
    node->prev->next = node->next;
    node->next->prev = node->prev;
}

// Insert node right after head (most recently used)
void insertAtHead(LRUCache* cache, Node* node) {
    node->next = cache->head->next;
    node->prev = cache->head;
    cache->head->next->prev = node;
    cache->head->next = node;
}

// Get value from cache
int lRUCacheGet(LRUCache* cache, int key) {
    int idx = hash(key);
    Node* node = cache->map[idx].node;

    while (node != NULL) {
        if (node->key == key) {
            removeNode(node);
            insertAtHead(cache, node); // move to MRU
            return node->value;
        }
        node = node->next;
    }
    return -1;
}

// Put key-value into cache
void lRUCachePut(LRUCache* cache, int key, int value) {
    int idx = hash(key);
    Node* node = cache->map[idx].node;

    // Check if key exists
    while (node != NULL) {
        if (node->key == key) {
            node->value = value;
            removeNode(node);
            insertAtHead(cache, node);
            return;
        }
        node = node->next;
    }

    // New entry
    Node* newNode = createNode(key, value);
    insertAtHead(cache, newNode);
    cache->map[idx].node = newNode;
    cache->size++;

    // If over capacity, evict LRU
    if (cache->size > cache->capacity) {
        Node* lru = cache->tail->prev;
        removeNode(lru);

        int lruIdx = hash(lru->key);
        cache->map[lruIdx].node = NULL;
        free(lru);
        cache->size--;
    }
}

// Free cache
void lRUCacheFree(LRUCache* cache) {
    Node* curr = cache->head;
    while (curr != NULL) {
        Node* temp = curr;
        curr = curr->next;
        free(temp);
    }
    free(cache->map);
    free(cache);
}

int main() {
    LRUCache* cache = lRUCacheCreate(2);

    lRUCachePut(cache, 1, 10);
    lRUCachePut(cache, 2, 20);

    printf("Get(1) = %d\n", lRUCacheGet(cache, 1)); // 10

    lRUCachePut(cache, 3, 30); // evicts key 2

    printf("Get(2) = %d\n", lRUCacheGet(cache, 2)); // -1
    printf("Get(3) = %d\n", lRUCacheGet(cache, 3)); // 30

    lRUCacheFree(cache);
    return 0;
}


```

## Example Run:

- Input/Operations:

```c

put(1, 10)
put(2, 20)
put(3, 30)
get(1) → 10
put(4, 40) → evicts key 2
get(2) → -1
get(3) → 30
get(4) → 40

```

## Output:

```c

Get(1): 10
Get(2): -1
Get(3): 30
Get(4): 40

```
