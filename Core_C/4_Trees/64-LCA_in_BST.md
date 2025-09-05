# Implement a program to find the Lowest Common Ancestor (LCA) of two nodes in a BST.

```c


#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

//  Utility function to create a new node 
struct Node* createNode(int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// Insert node into BST 
struct Node* insert(struct Node* root, int value) {
    if (root == NULL) return createNode(value);

    if (value < root->data)
        root->left = insert(root->left, value);
    else if (value > root->data)
        root->right = insert(root->right, value);

    return root;
}

// Find LCA of two nodes 
struct Node* findLCA(struct Node* root, int n1, int n2) {
    if (root == NULL) return NULL;

    // If both values are smaller, LCA is in left subtree
    if (n1 < root->data && n2 < root->data)
        return findLCA(root->left, n1, n2);

    // If both values are greater, LCA is in right subtree
    if (n1 > root->data && n2 > root->data)
        return findLCA(root->right, n1, n2);

    // Otherwise, root is the LCA
    return root;
}

int main() {
    /*
        Example BST:
                 20
                /  \
              10    30
             / \    / \
            5  15  25  35

        LCA(5, 15) = 10
        LCA(5, 30) = 20
    */

    struct Node* root = NULL;
    root = insert(root, 20);
    insert(root, 10);
    insert(root, 30);
    insert(root, 5);
    insert(root, 15);
    insert(root, 25);
    insert(root, 35);

    int n1 = 5, n2 = 15;
    struct Node* lca = findLCA(root, n1, n2);
    if (lca != NULL)
        printf("LCA of %d and %d is %d\n", n1, n2, lca->data);

    n1 = 5, n2 = 30;
    lca = findLCA(root, n1, n2);
    if (lca != NULL)
        printf("LCA of %d and %d is %d\n", n1, n2, lca->data);

    return 0;
}


```

## Example Output:

```c
LCA of 5 and 15 is 10
LCA of 5 and 30 is 20
```
