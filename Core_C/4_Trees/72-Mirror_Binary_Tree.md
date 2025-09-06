# Implement a program to mirror a binary tree.

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

// Insert into BST (helper to build a tree)
struct Node* insert(struct Node* root, int value) {
    if (root == NULL) return createNode(value);

    if (value < root->data)
        root->left = insert(root->left, value);
    else if (value > root->data)
        root->right = insert(root->right, value);

    return root;
}

// Inorder Traversal
void inorder(struct Node* root) {
    if (root != NULL) {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

// Mirror the binary tree
void mirrorTree(struct Node* root) {
    if (root == NULL) return;

    // Swap left and right
    struct Node* temp = root->left;
    root->left = root->right;
    root->right = temp;

    // Recur for subtrees
    mirrorTree(root->left);
    mirrorTree(root->right);
}

int main() {
    /*
            Original BST:
                  10
                 /  \
                5    20
               / \   / \
              3   7 15  25
    */

    struct Node* root = NULL;
    root = insert(root, 10);
    insert(root, 5);
    insert(root, 20);
    insert(root, 3);
    insert(root, 7);
    insert(root, 15);
    insert(root, 25);

    printf("Inorder Traversal of Original Tree: ");
    inorder(root);
    printf("\n");

    // Mirror the tree
    mirrorTree(root);

    /*
            Mirrored Tree:
                  10
                 /  \
                20   5
               / \   / \
              25 15 7   3
    */

    printf("Inorder Traversal of Mirrored Tree: ");
    inorder(root);
    printf("\n");

    return 0;
}


```

## 🎯 Example Output

```c

Inorder Traversal of Original Tree: 3 5 7 10 15 20 25 
Inorder Traversal of Mirrored Tree: 25 20 15 10 7 5 3 

```
