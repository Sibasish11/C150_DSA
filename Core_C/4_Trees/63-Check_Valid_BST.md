# Write a program to check if a given Binary Tree is a valid Binary Search Tree.

```c

#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

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

// Helper function to check BST validity 
int isBSTUtil(struct Node* root, int min, int max) {
    if (root == NULL)
        return 1; // Empty tree is valid BST

    if (root->data <= min || root->data >= max)
        return 0; // Violates BST property

    return isBSTUtil(root->left, min, root->data) &&
           isBSTUtil(root->right, root->data, max);
}

// Main BST check function 
int isBST(struct Node* root) {
    return isBSTUtil(root, INT_MIN, INT_MAX);
}

int main() {
    /*
       Example 1: Valid BST
            5
           / \
          3   7
         / \   \
        2   4   8
    */
    struct Node* root1 = createNode(5);
    root1->left = createNode(3);
    root1->right = createNode(7);
    root1->left->left = createNode(2);
    root1->left->right = createNode(4);
    root1->right->right = createNode(8);

    printf("Tree 1 is %s\n", isBST(root1) ? "a valid BST" : "NOT a valid BST");

    /*
       Example 2: Invalid BST
            5
           / \
          3   7
         / \
        2   6   <-- violates BST (6 in left subtree of 5)
    */
    struct Node* root2 = createNode(5);
    root2->left = createNode(3);
    root2->right = createNode(7);
    root2->left->left = createNode(2);
    root2->left->right = createNode(6);

    printf("Tree 2 is %s\n", isBST(root2) ? "a valid BST" : "NOT a valid BST");

    return 0;
}

```

## Example Output:

```c

Tree 1 is a valid BST
Tree 2 is NOT a valid BST

```
