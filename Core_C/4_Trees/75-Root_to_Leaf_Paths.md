# Implement a program to find all paths from the root to leaf in a binary tree.

```c

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* left;
    struct Node* right;
};

struct Node* createNode(int value) {
    struct Node* node = (struct Node*)malloc(sizeof(struct Node));
    node->data = value;
    node->left = node->right = NULL;
    return node;
}

// Utility function to print a path
void printPath(int path[], int pathLen) {
    for (int i = 0; i < pathLen; i++) {
        printf("%d ", path[i]);
    }
    printf("\n");
}

// Recursive function to find all root-to-leaf paths
void findPaths(struct Node* root, int path[], int pathLen) {
    if (root == NULL) return;

    // Add current node to path
    path[pathLen] = root->data;
    pathLen++;

    // If leaf node -> print the path
    if (root->left == NULL && root->right == NULL) {
        printPath(path, pathLen);
    } else {
        // Recurse left and right
        findPaths(root->left, path, pathLen);
        findPaths(root->right, path, pathLen);
    }
}

int main() {
    /*
            Example Tree:
                   1
                 /   \
                2     3
               / \     \
              4   5     6

        Paths:
        1 2 4
        1 2 5
        1 3 6
    */

    struct Node* root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);
    root->right->right = createNode(6);

    int path[100]; // max path length
    printf("All root-to-leaf paths:\n");
    findPaths(root, path, 0);

    return 0;
}


```

## Example Output:

```c
All root-to-leaf paths:
1 2 4
1 2 5
1 3 6
```
