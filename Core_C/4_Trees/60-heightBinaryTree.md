# Write a program to find the height of a Binary Tree.

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

// Recursive function to calculate height 
int height(struct Node* root) {
    if (root == NULL)
        return -1; // convention: height of empty tree = -1
    else {
        int leftHeight = height(root->left);
        int rightHeight = height(root->right);

        // Return the larger height + 1
        return (leftHeight > rightHeight ? leftHeight : rightHeight) + 1;
    }
}

int main() {
    /*
       Example Tree:
            1
           / \
          2   3
         / \
        4   5
    */
    struct Node* root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);

    printf("Height of the Binary Tree: %d\n", height(root));

    return 0;
}


```

## Example Output:
```c

Height of the Binary Tree: 2

```
