# Write a program to find the in-order successor and predecessor of a given node in a BST.
  
   - Successor: smallest node greater than the key
   - Predecessor: largest node smaller than the key
   - Time Complexity: O(h), where h is height of the BST


```c

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// Create New Node 
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

// Find Minimum Node 
struct Node* findMin(struct Node* node) {
    while (node && node->left != NULL)
        node = node->left;
    return node;
}

// Find Maximum Node 
struct Node* findMax(struct Node* node) {
    while (node && node->right != NULL)
        node = node->right;
    return node;
}

// Find In-order Successor 
struct Node* findSuccessor(struct Node* root, struct Node* target) {
    if (target->right != NULL) 
        return findMin(target->right);

    struct Node* successor = NULL;
    while (root != NULL) {
        if (target->data < root->data) {
            successor = root;
            root = root->left;
        } else if (target->data > root->data) {
            root = root->right;
        } else break;
    }
    return successor;
}

// Find In-order Predecessor 
struct Node* findPredecessor(struct Node* root, struct Node* target) {
    if (target->left != NULL) 
        return findMax(target->left);

    struct Node* predecessor = NULL;
    while (root != NULL) {
        if (target->data > root->data) {
            predecessor = root;
            root = root->right;
        } else if (target->data < root->data) {
            root = root->left;
        } else break;
    }
    return predecessor;
}

// Search a Node 
struct Node* search(struct Node* root, int key) {
    if (root == NULL || root->data == key) return root;
    if (key < root->data) return search(root->left, key);
    return search(root->right, key);
}

int main() {
    /*
        Example BST:
                 20
                /  \
              10    30
             / \    / \
            5  15  25  35
    */

    struct Node* root = NULL;
    root = insert(root, 20);
    insert(root, 10);
    insert(root, 30);
    insert(root, 5);
    insert(root, 15);
    insert(root, 25);
    insert(root, 35);

    int key = 20;
    struct Node* target = search(root, key);

    if (target) {
        struct Node* succ = findSuccessor(root, target);
        struct Node* pred = findPredecessor(root, target);

        if (pred) printf("Predecessor of %d is %d\n", key, pred->data);
        else printf("No predecessor exists for %d\n", key);

        if (succ) printf("Successor of %d is %d\n", key, succ->data);
        else printf("No successor exists for %d\n", key);
    } else {
        printf("Key %d not found in BST\n", key);
    }

    return 0;
}

```

## Example Output:

```c

Node: 20
In-order Successor: 25
In-order Predecessor: 15

```
