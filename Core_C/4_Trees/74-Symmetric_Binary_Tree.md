# Write a program to check if a binary tree is symmetric.

```c

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// Create a new node
struct Node* createNode(int value) {
    struct Node* node = (struct Node*)malloc(sizeof(struct Node));
    node->data = value;
    node->left = node->right = NULL;
    return node;
}

// Insert into BST (for building tree, not necessarily symmetric)
struct Node* insert(struct Node* root, int value) {
    if (root == NULL) return createNode(value);

    if (value < root->data)
        root->left = insert(root->left, value);
    else if (value > root->data)
        root->right = insert(root->right, value);

    return root;
}

// Check if two subtrees are mirrors
int isMirror(struct Node* t1, struct Node* t2) {
    if (t1 == NULL && t2 == NULL) return 1;
    if (t1 == NULL || t2 == NULL) return 0;

    return (t1->data == t2->data) &&
           isMirror(t1->left, t2->right) &&
           isMirror(t1->right, t2->left);
}

// Check if the tree is symmetric
int isSymmetric(struct Node* root) {
    if (root == NULL) return 1; // Empty tree is symmetric
    return isMirror(root->left, root->right);
}

int main() {
    /*
            Example Symmetric Tree:
                   1
                 /   \
                2     2
               / \   / \
              3   4 4   3
    */

    struct Node* root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(2);
    root->left->left = createNode(3);
    root->left->right = createNode(4);
    root->right->left = createNode(4);
    root->right->right = createNode(3);

    if (isSymmetric(root))
        printf("The tree is symmetric.\n");
    else
        printf("The tree is NOT symmetric.\n");

    return 0;
}


```

## Output:
```c
The tree is symmetric.
```

## If you changed one of the subtrees (e.g., removed a node), it would print:

```c
The tree is NOT symmetric.
```
