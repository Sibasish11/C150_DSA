# Write a program to balance a BST (e.g., by converting to sorted array, then to balanced BST).

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
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->left = newNode->right = NULL;
    return newNode;
}

// Insert into BST
struct Node* insert(struct Node* root, int value) {
    if (root == NULL) return createNode(value);
    if (value < root->data)
        root->left = insert(root->left, value);
    else if (value > root->data)
        root->right = insert(root->right, value);
    return root;
}

// -------- Step 1: Store inorder traversal in array --------
void storeInorder(struct Node* root, int inorder[], int* index) {
    if (root == NULL) return;
    storeInorder(root->left, inorder, index);
    inorder[(*index)++] = root->data;
    storeInorder(root->right, inorder, index);
}

// -------- Step 2: Build Balanced BST from sorted array --------
struct Node* buildBalancedBST(int inorder[], int start, int end) {
    if (start > end) return NULL;

    int mid = (start + end) / 2;
    struct Node* root = createNode(inorder[mid]);

    root->left = buildBalancedBST(inorder, start, mid - 1);
    root->right = buildBalancedBST(inorder, mid + 1, end);

    return root;
}

// Utility: Count nodes
int countNodes(struct Node* root) {
    if (root == NULL) return 0;
    return 1 + countNodes(root->left) + countNodes(root->right);
}

// Print Inorder (to check balance)
void printInorder(struct Node* root) {
    if (root == NULL) return;
    printInorder(root->left);
    printf("%d ", root->data);
    printInorder(root->right);
}

int main() {
    /*
        Example: Skewed BST (unbalanced)
                10
                  \
                   20
                     \
                      30
                        \
                         40
    */

    struct Node* root = NULL;
    root = insert(root, 10);
    insert(root, 20);
    insert(root, 30);
    insert(root, 40);

    printf("Inorder of Original (Unbalanced) BST: ");
    printInorder(root);
    printf("\n");

    int n = countNodes(root);
    int* inorder = (int*)malloc(n * sizeof(int));
    int index = 0;

    storeInorder(root, inorder, &index);

    root = buildBalancedBST(inorder, 0, n - 1);

    printf("Inorder of Balanced BST: ");
    printInorder(root);
    printf("\n");

    free(inorder);
    return 0;
}


```

## Sample Input / Output

- Original Unbalanced BST (Skewed):
```c
10 -> 20 -> 30 -> 40
```

## Output:

```c
Inorder of Original (Unbalanced) BST: 10 20 30 40 
Inorder of Balanced BST: 10 20 30 40
```

## Balanced BST Structure:

```c

       20
      /  \
    10    30
            \
             40

```
