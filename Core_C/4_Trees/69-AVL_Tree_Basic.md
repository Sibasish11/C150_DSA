# Implement a basic AVL Tree with insertion and rotation operations. (Focus on understanding the balancing logic).

```c

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
    int height;
};

// Get height of node
int height(struct Node* n) {
    if (n == NULL) return 0;
    return n->height;
}

// Get max of two integers
int max(int a, int b) {
    return (a > b) ? a : b;
}

// Create a new node
struct Node* createNode(int value) {
    struct Node* node = (struct Node*)malloc(sizeof(struct Node));
    node->data = value;
    node->left = node->right = NULL;
    node->height = 1;
    return node;
}

// Right rotate (LL case)
struct Node* rightRotate(struct Node* y) {
    struct Node* x = y->left;
    struct Node* T2 = x->right;

    // Rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    return x; // new root
}

// Left rotate (RR case)
struct Node* leftRotate(struct Node* x) {
    struct Node* y = x->right;
    struct Node* T2 = y->left;

    // Rotation
    y->left = x;
    x->right = T2;

    // Update heights
    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    return y; // new root
}

// Get balance factor
int getBalance(struct Node* n) {
    if (n == NULL) return 0;
    return height(n->left) - height(n->right);
}

// Insert into AVL tree
struct Node* insert(struct Node* node, int key) {
    // 1. Normal BST insert
    if (node == NULL) return createNode(key);

    if (key < node->data)
        node->left = insert(node->left, key);
    else if (key > node->data)
        node->right = insert(node->right, key);
    else // Equal keys not allowed
        return node;

    // 2. Update height
    node->height = 1 + max(height(node->left), height(node->right));

    // 3. Get balance factor
    int balance = getBalance(node);

    // 4. Balance the tree with rotations

    // Case 1: Left Left
    if (balance > 1 && key < node->left->data)
        return rightRotate(node);

    // Case 2: Right Right
    if (balance < -1 && key > node->right->data)
        return leftRotate(node);

    // Case 3: Left Right
    if (balance > 1 && key > node->left->data) {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    // Case 4: Right Left
    if (balance < -1 && key < node->right->data) {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    return node; // unchanged
}

// Print preorder traversal
void preOrder(struct Node* root) {
    if (root != NULL) {
        printf("%d ", root->data);
        preOrder(root->left);
        preOrder(root->right);
    }
}

int main() {
    struct Node* root = NULL;

    /* Insert nodes */
    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    printf("Preorder traversal of AVL tree: ");
    preOrder(root);
    printf("\n");

    return 0;
}


```

## Sample Output:

```c

Preorder traversal of AVL tree: 30 20 10 25 40 50

```

### Balanced AVL Tree structure:

```c
        30
       /  \
     20    40
    / \      \
  10  25     50

```
