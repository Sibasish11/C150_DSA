# Implement a program to convert a BST into a sorted Singly Linked List.

```c

#include <stdio.h>
#include <stdlib.h>

// Node Structure (for both BST & Linked List) 
struct Node {
    int data;
    struct Node* left;
    struct Node* right; // In linked list, 'right' will act as 'next'
};

// Create a new BST node
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

// Global pointers to track head & previous node of linked list
struct Node* head = NULL;
struct Node* prev = NULL;

// Convert BST to Sorted Linked List using inorder traversal
void BSTtoSortedLinkedList(struct Node* root) {
    if (root == NULL) return;

    // Left subtree
    BSTtoSortedLinkedList(root->left);

    // Process current node
    if (prev == NULL) {
        head = root;  // First node becomes head
    } else {
        prev->right = root;  // Link previous node with current
    }
    root->left = NULL; // Ensure left pointer is NULL
    prev = root;       // Move prev to current

    // Right subtree
    BSTtoSortedLinkedList(root->right);
}

// Print Linked List
void printLinkedList(struct Node* head) {
    struct Node* temp = head;
    while (temp != NULL) {
        printf("%d -> ", temp->data);
        temp = temp->right;
    }
    printf("NULL\n");
}

int main() {
    /*
        Example BST:
                 8
                / \
               4   12
              / \  / \
             2  6 10 14
    */

    struct Node* root = NULL;
    root = insert(root, 8);
    insert(root, 4);
    insert(root, 12);
    insert(root, 2);
    insert(root, 6);
    insert(root, 10);
    insert(root, 14);

    BSTtoSortedLinkedList(root);

    printf("Sorted Linked List from BST: ");
    printLinkedList(head);

    return 0;
}


```

## Output Linked List:

```c

Sorted Linked List from BST: 2 -> 4 -> 6 -> 8 -> 10 -> 12 -> 14 -> NULL

```
