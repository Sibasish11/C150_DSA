# Implement a Binary Tree node structure.

- Each node contains:

   * Data (integer for simplicity)

   * Pointer to left child

   * Pointer to right child

- Example main() creates a small tree manually.

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

int main() {
    // Manually creating a binary tree:
    //         1
    //        / \
    //       2   3
    //      / \
    //     4   5

    struct Node* root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);

    printf("Root: %d\n", root->data);
    printf("Left Child of Root: %d\n", root->left->data);
    printf("Right Child of Root: %d\n", root->right->data);

    return 0;

}

```

# Example Output:

```c

Root: 1
Left Child of Root: 2
Right Child of Root: 3

```
