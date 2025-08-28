# Write a program to implement a Circular Linked List. Include functions for insertion and deletion.


## Concept:

- In Circular Linked List (CLL), the last node points back to the head.
- Insertion:
    - If empty: new node points to itself.
    - Else: Insert at end (before head) and update links.
- Deletion:
    - If only one node: free it and set head = NULL.
    - Else: Search node, adjust previous node's next, free the node.
- Traversal:
    - Start at head, move until back to head again.

```c

#include <stdio.h>
#include <stdlib.h>

// Define Node
struct Node {
    int data;
    struct Node* next;
};

// Create new node
struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->next = NULL;
    return newNode;
}

// Insert at end
void insert(struct Node** head, int data) {
    struct Node* newNode = createNode(data);
    if (*head == NULL) {
        *head = newNode;
        newNode->next = *head; // Points to itself
        return;
    }
    struct Node* temp = *head;
    while (temp->next != *head) {
        temp = temp->next;
    }
    temp->next = newNode;
    newNode->next = *head;
}

// Delete by value
void deleteNode(struct Node** head, int key) {
    if (*head == NULL) {
        printf("List is empty. Nothing to delete.\n");
        return;
    }

    struct Node *curr = *head, *prev = NULL;

    // Case: only one node
    if (curr->data == key && curr->next == *head) {
        free(curr);
        *head = NULL;
        return;
    }

    // Find node to delete
    do {
        if (curr->data == key) break;
        prev = curr;
        curr = curr->next;
    } while (curr != *head);

    // Node not found
    if (curr->data != key) {
        printf("Value %d not found in the list.\n", key);
        return;
    }

    // If deleting head
    if (curr == *head) {
        prev = *head;
        while (prev->next != *head) {
            prev = prev->next;
        }
        *head = curr->next;
        prev->next = *head;
        free(curr);
    }
    // Else deleting middle/last node
    else {
        prev->next = curr->next;
        free(curr);
    }
}

// Traversal
void traverse(struct Node* head) {
    if (head == NULL) {
        printf("List is empty.\n");
        return;
    }
    struct Node* temp = head;
    printf("Circular List: ");
    do {
        printf("%d -> ", temp->data);
        temp = temp->next;
    } while (temp != head);
    printf("(back to head)\n");
}

// Main
int main() {
    struct Node* head = NULL;

    insert(&head, 10);
    insert(&head, 20);
    insert(&head, 30);
    insert(&head, 40);

    traverse(head);

    printf("\nDeleting 20...\n");
    deleteNode(&head, 20);
    traverse(head);

    printf("\nDeleting 10...\n");
    deleteNode(&head, 10);
    traverse(head);

    printf("\nDeleting 100...\n");
    deleteNode(&head, 100);

    printf("\nDeleting 30...\n");
    deleteNode(&head, 30);
    traverse(head);

    printf("\nDeleting 40...\n");
    deleteNode(&head, 40);
    traverse(head);

    return 0;
}

```

## Sample Output:

```c

Circular List: 10 -> 20 -> 30 -> 40 -> (back to head)

Deleting 20...
Circular List: 10 -> 30 -> 40 -> (back to head)

Deleting 10...
Circular List: 30 -> 40 -> (back to head)

Deleting 100...
Value 100 not found in the list.

Deleting 30...
Circular List: 40 -> (back to head)

Deleting 40...
List is empty.


```
