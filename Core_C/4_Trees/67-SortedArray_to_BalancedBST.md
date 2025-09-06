# Develop a program to convert a sorted array into a Balanced Binary Search Tree (e.g., using a recursive approach similar to constructing a minimal height BST).

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

// Recursive function: Convert sorted array to Balanced BST
struct Node* sortedArrayToBalancedBST(int arr[], int start, int end) {
    if (start > end) return NULL;

    // Pick middle element as root
    int mid = (start + end) / 2;
    struct Node* root = createNode(arr[mid]);

    // Recursively construct left and right subtrees
    root->left = sortedArrayToBalancedBST(arr, start, mid - 1);
    root->right = sortedArrayToBalancedBST(arr, mid + 1, end);

    return root;
}

// Inorder Traversal (should print sorted array)
void inorderTraversal(struct Node* root) {
    if (root == NULL) return;
    inorderTraversal(root->left);
    printf("%d ", root->data);
    inorderTraversal(root->right);
}

// Preorder Traversal (to show tree structure)
void preorderTraversal(struct Node* root) {
    if (root == NULL) return;
    printf("%d ", root->data);
    preorderTraversal(root->left);
    preorderTraversal(root->right);
}

int main() {
    int arr[] = {2, 4, 6, 8, 10, 12, 14};
    int n = sizeof(arr) / sizeof(arr[0]);

    struct Node* root = sortedArrayToBalancedBST(arr, 0, n - 1);

    printf("Inorder Traversal (sorted array): ");
    inorderTraversal(root);
    printf("\n");

    printf("Preorder Traversal (tree structure): ");
    preorderTraversal(root);
    printf("\n");

    return 0;
}


```

## Sample Input / Output:

- Input Array:

```c
[2, 4, 6, 8, 10, 12, 14]
```

## Output:
```c
Inorder Traversal (sorted array): 2 4 6 8 10 12 14 
Preorder Traversal (tree structure): 8 4 2 6 12 10 14 
```
