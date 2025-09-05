# Implement a program to perform Level-order (BFS) traversal of a Binary Tree.

```c 

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// Utility function to create a new node 
struct Node* createNode(int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

// Queue Implementation 
struct Queue {
    int front, rear, size;
    unsigned capacity;
    struct Node** array;
};

// Create Queue
struct Queue* createQueue(unsigned capacity) {
    struct Queue* queue = (struct Queue*)malloc(sizeof(struct Queue));
    queue->capacity = capacity;
    queue->front = queue->size = 0;
    queue->rear = capacity - 1;
    queue->array = (struct Node**)malloc(queue->capacity * sizeof(struct Node*));
    return queue;
}

int isEmpty(struct Queue* queue) {
    return (queue->size == 0);
}

int isFull(struct Queue* queue) {
    return (queue->size == queue->capacity);
}

void enqueue(struct Queue* queue, struct Node* item) {
    if (isFull(queue)) return; // Overflow check
    queue->rear = (queue->rear + 1) % queue->capacity;
    queue->array[queue->rear] = item;
    queue->size++;
}

struct Node* dequeue(struct Queue* queue) {
    if (isEmpty(queue)) return NULL; // Underflow check
    struct Node* item = queue->array[queue->front];
    queue->front = (queue->front + 1) % queue->capacity;
    queue->size--;
    return item;
}

// Level-order Traversal 
void levelOrder(struct Node* root) {
    if (root == NULL) return;

    // Create a queue with large enough capacity
    struct Queue* queue = createQueue(100);

    enqueue(queue, root);

    while (!isEmpty(queue)) {
        struct Node* current = dequeue(queue);
        printf("%d ", current->data);

        if (current->left != NULL)
            enqueue(queue, current->left);
        if (current->right != NULL)
            enqueue(queue, current->right);
    }
}

int main() {
    /*
       Example Tree:
            1
           / \
          2   3
         / \
        4   5
    */
    struct Node* root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);

    printf("Level-order Traversal: ");
    levelOrder(root);
    printf("\n");

    return 0;
}


```

## Example Output:

```c

Level-order Traversal: 1 2 3 4 5

```
