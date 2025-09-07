# Develop a program to serialize and deserialize a binary tree.

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

// Serialize the tree into an array
void serialize(struct Node* root, FILE* file) {
    if (root == NULL) {
        fprintf(file, "-1 "); // -1 denotes NULL
        return;
    }
    fprintf(file, "%d ", root->data);
    serialize(root->left, file);
    serialize(root->right, file);
}

// Deserialize the tree from an array
struct Node* deserialize(FILE* file) {
    int val;
    if (fscanf(file, "%d", &val) != 1 || val == -1) {
        return NULL;
    }

    struct Node* root = createNode(val);
    root->left = deserialize(file);
    root->right = deserialize(file);
    return root;
}

// Inorder Traversal (for verification)
void inorder(struct Node* root) {
    if (root != NULL) {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

int main() {
    /*
            Example BST:
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

    // Serialize into file
    FILE* file = fopen("tree.txt", "w");
    if (file == NULL) {
        printf("Error opening file!\n");
        return 1;
    }
    serialize(root, file);
    fclose(file);

    printf("Tree serialized into tree.txt\n");

    // Deserialize from file
    file = fopen("tree.txt", "r");
    if (file == NULL) {
        printf("Error opening file!\n");
        return 1;
    }
    struct Node* newRoot = deserialize(file);
    fclose(file);

    printf("Inorder traversal of deserialized tree: ");
    inorder(newRoot);
    printf("\n");

    return 0;
}


```

## Example Output:

```c
Tree serialized into tree.txt
Inorder traversal of deserialized tree: 3 5 7 10 15 20 25
```

### And the tree.txt file will contain something like:

```c
10 5 3 -1 -1 7 -1 -1 20 15 -1 -1 25 -1 -1
```
