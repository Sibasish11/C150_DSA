# Implement a program to construct a BST from a sorted array.

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
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// Construct BST from sorted array
struct Node* sortedArrayToBST(int arr[], int start, int end) {
    if (start > end) return NULL;

    // Middle element as root
    int mid = (start + end) / 2;
    struct Node* root = createNode(arr[mid]);

    // Recursively build left and right subtrees
    root->left = sortedArrayToBST(arr, start, mid - 1);
    root->right = sortedArrayToBST(arr, mid + 1, end);

    return root;
}

// Inorder Traversal (should print sorted order)
void inorderTraversal(struct Node* root) {
    if (root == NULL) return;
    inorderTraversal(root->left);
    printf("%d ", root->data);
    inorderTraversal(root->right);
}

// Preorder Traversal (to show structure of BST)
void preorderTraversal(struct Node* root) {
    if (root == NULL) return;
    printf("%d ", root->data);
    preorderTraversal(root->left);
    preorderTraversal(root->right);
}

int main() {
    int arr[] = {1, 2, 3, 4, 5, 6, 7};
    int n = sizeof(arr) / sizeof(arr[0]);

    struct Node* root = sortedArrayToBST(arr, 0, n - 1);

    printf("Inorder Traversal of constructed BST: ");
    inorderTraversal(root);
    printf("\n");

    printf("Preorder Traversal of constructed BST: ");
    preorderTraversal(root);
    printf("\n");

    return 0;
}


```

## Sample Input / Output

- Input Array:

```c

[1, 2, 3, 4, 5, 6, 7]

```

### Output:

```c

Inorder Traversal of constructed BST: 1 2 3 4 5 6 7 
Preorder Traversal of constructed BST: 4 2 1 3 6 5 7 


```
