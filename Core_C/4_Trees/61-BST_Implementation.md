# 61.Design and implement a Binary Search Tree (BST). Include functions for: a) Insertion of a node. b) Searching for a node. c) Deletion of a node. d) Finding minimum and maximum elements. 

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
    newNode->left = newNode->right = NULL;
    return newNode;
}

// (a) Insert a node 
struct Node* insert(struct Node* root, int value) {
    if (root == NULL) return createNode(value);

    if (value < root->data)
        root->left = insert(root->left, value);
    else if (value > root->data)
        root->right = insert(root->right, value);

    return root; // unchanged pointer
}

// (b) Search for a node 
struct Node* search(struct Node* root, int key) {
    if (root == NULL || root->data == key)
        return root;

    if (key < root->data)
        return search(root->left, key);

    return search(root->right, key);
}

// Find minimum 
struct Node* findMin(struct Node* root) {
    while (root && root->left != NULL)
        root = root->left;
    return root;
}

// Find maximum 
struct Node* findMax(struct Node* root) {
    while (root && root->right != NULL)
        root = root->right;
    return root;
}

// (c) Delete a node 
struct Node* deleteNode(struct Node* root, int key) {
    if (root == NULL) return root;

    if (key < root->data)
        root->left = deleteNode(root->left, key);
    else if (key > root->data)
        root->right = deleteNode(root->right, key);
    else {
        // Case 1: No child
        if (root->left == NULL && root->right == NULL) {
            free(root);
            return NULL;
        }
        // Case 2: One child
        else if (root->left == NULL) {
            struct Node* temp = root->right;
            free(root);
            return temp;
        }
        else if (root->right == NULL) {
            struct Node* temp = root->left;
            free(root);
            return temp;
        }
        // Case 3: Two children
        struct Node* temp = findMin(root->right);
        root->data = temp->data;
        root->right = deleteNode(root->right, temp->data);
    }
    return root;
}

void inorder(struct Node* root) {
    if (root != NULL) {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

int main() {
    struct Node* root = NULL;

    // Insert nodes
    root = insert(root, 50);
    root = insert(root, 30);
    root = insert(root, 70);
    root = insert(root, 20);
    root = insert(root, 40);
    root = insert(root, 60);
    root = insert(root, 80);

    printf("In-order Traversal of BST: ");
    inorder(root);
    printf("\n");

    // Search
    int key = 40;
    struct Node* found = search(root, key);
    if (found != NULL)
        printf("Element %d found in BST.\n", key);
    else
        printf("Element %d not found in BST.\n", key);

    // Find min and max
    printf("Minimum element: %d\n", findMin(root)->data);
    printf("Maximum element: %d\n", findMax(root)->data);

    // Delete a node
    root = deleteNode(root, 30);
    printf("In-order after deleting 30: ");
    inorder(root);
    printf("\n");

    return 0;
}

```

## Example Output:

```c
In-order Traversal of BST: 20 30 40 50 60 70 80 
Element 40 found in BST.
Minimum element: 20
Maximum element: 80
In-order after deleting 30: 20 40 50 60 70 80 
```
