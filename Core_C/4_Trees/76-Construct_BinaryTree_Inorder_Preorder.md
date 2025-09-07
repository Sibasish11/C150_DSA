# Develop a program to construct a binary tree from its in-order and pre-order traversals.

```c

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// Create new node
struct Node* createNode(int value) {
    struct Node* node = (struct Node*)malloc(sizeof(struct Node));
    node->data = value;
    node->left = node->right = NULL;
    return node;
}

// Find index of value in inorder[]
int search(int inorder[], int start, int end, int value) {
    for (int i = start; i <= end; i++) {
        if (inorder[i] == value)
            return i;
    }
    return -1;
}

// Recursive function to build tree
struct Node* buildTree(int inorder[], int preorder[], int inStart, int inEnd, int* preIndex) {
    if (inStart > inEnd) return NULL;

    // Get current node from preorder
    int curr = preorder[*preIndex];
    (*preIndex)++;
    struct Node* node = createNode(curr);

    // If leaf node
    if (inStart == inEnd) return node;

    // Find index of current node in inorder[]
    int inIndex = search(inorder, inStart, inEnd, curr);

    // Build left and right subtrees
    node->left = buildTree(inorder, preorder, inStart, inIndex - 1, preIndex);
    node->right = buildTree(inorder, preorder, inIndex + 1, inEnd, preIndex);

    return node;
}

// Print tree (Inorder Traversal)
void printInorder(struct Node* root) {
    if (root == NULL) return;
    printInorder(root->left);
    printf("%d ", root->data);
    printInorder(root->right);
}

// Print tree (Preorder Traversal)
void printPreorder(struct Node* root) {
    if (root == NULL) return;
    printf("%d ", root->data);
    printPreorder(root->left);
    printPreorder(root->right);
}

int main() {
    /*
        Example:
        Inorder   = [4, 2, 5, 1, 6, 3]
        Preorder  = [1, 2, 4, 5, 3, 6]

        Constructed Binary Tree:
                 1
               /   \
              2     3
             / \     \
            4   5     6
    */

    int inorder[] = {4, 2, 5, 1, 6, 3};
    int preorder[] = {1, 2, 4, 5, 3, 6};
    int n = sizeof(inorder) / sizeof(inorder[0]);
    int preIndex = 0;

    struct Node* root = buildTree(inorder, preorder, 0, n - 1, &preIndex);

    printf("Inorder of constructed tree: ");
    printInorder(root);
    printf("\n");

    printf("Preorder of constructed tree: ");
    printPreorder(root);
    printf("\n");

    return 0;
}


```

## 🎯 Example Output:

```c

Inorder of constructed tree: 4 2 5 1 6 3 
Preorder of constructed tree: 1 2 4 5 3 6 

```
