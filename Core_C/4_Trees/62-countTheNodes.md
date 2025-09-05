# Implement a program to count the number of nodes in a Binary Tree.

```c

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

// Utility function to create a new node 
struct Node* createNode(int value) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

// -------- Recursive function to count nodes --------
int countNodes(struct Node* root) {
    if (root == NULL)
        return 0;
    return 1 + countNodes(root->left) + countNodes(root->right);
}

int main() {
    /*
       Example Tree:
            1
           / \
          2   3
         / \
        4   5

       Total nodes = 5
    */
    struct Node* root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);

    printf("Number of nodes in the Binary Tree: %d\n", countNodes(root));

    return 0;
}

```

## Example Output:

```c

Number of nodes in the Binary Tree: 5

```
