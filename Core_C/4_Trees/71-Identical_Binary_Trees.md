# Write a program to find if two binary trees are identical.

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

// Insert into BST (helper to build trees)
struct Node* insert(struct Node* root, int value) {
    if (root == NULL) return createNode(value);

    if (value < root->data)
        root->left = insert(root->left, value);
    else if (value > root->data)
        root->right = insert(root->right, value);

    return root;
}

// Check if two trees are identical
int areIdentical(struct Node* root1, struct Node* root2) {
    if (root1 == NULL && root2 == NULL) 
        return 1;  // Both empty → identical

    if (root1 == NULL || root2 == NULL) 
        return 0;  // One empty → not identical

    return (root1->data == root2->data) &&
           areIdentical(root1->left, root2->left) &&
           areIdentical(root1->right, root2->right);
}

int main() {
    struct Node* root1 = NULL;
    struct Node* root2 = NULL;

    // Tree 1
    root1 = insert(root1, 10);
    insert(root1, 5);
    insert(root1, 15);

    // Tree 2
    root2 = insert(root2, 10);
    insert(root2, 5);
    insert(root2, 15);

    if (areIdentical(root1, root2))
        printf("The two trees are identical.\n");
    else
        printf("The two trees are NOT identical.\n");

    return 0;
}

```

## Example Output:

```c

The two trees are identical.

```
