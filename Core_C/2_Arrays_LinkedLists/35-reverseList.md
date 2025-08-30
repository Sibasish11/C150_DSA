# Write a program to reverse a Doubly Linked List.

```c

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* prev;
    struct Node* next;
};

// Function to create a new node
struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->prev = NULL;
    newNode->next = NULL;
    return newNode;
}

// Insert at end
void insertEnd(struct Node** head, int data) {
    struct Node* newNode = createNode(data);
    if (*head == NULL) {
        *head = newNode;
        return;
    }
    struct Node* temp = *head;
    while (temp->next != NULL) temp = temp->next;
    temp->next = newNode;
    newNode->prev = temp;
}

// Function to reverse a DLL
void reverseList(struct Node** head) {
    struct Node* temp = NULL;
    struct Node* current = *head;

    // Swap next and prev for all nodes
    while (current != NULL) {
        temp = current->prev;
        current->prev = current->next;
        current->next = temp;
        current = current->prev;  // Move to "next" node (previous in original list)
    }

    // Update head (before exiting, temp is at last valid node)
    if (temp != NULL) {
        *head = temp->prev;
    }
}

// Print DLL
void traverse(struct Node* head) {
    while (head != NULL) {
        printf("%d <-> ", head->data);
        head = head->next;
    }
    printf("NULL\n");
}

int main() {
    struct Node* head = NULL;

    // Example DLL: 1 <-> 2 <-> 3 <-> 4 <-> 5
    insertEnd(&head, 1);
    insertEnd(&head, 2);
    insertEnd(&head, 3);
    insertEnd(&head, 4);
    insertEnd(&head, 5);

    printf("Original List: ");
    traverse(head);

    reverseList(&head);

    printf("Reversed List: ");
    traverse(head);

    return 0;
}

```

### 📌 Sample Output:

```c 

Original List: 1 <-> 2 <-> 3 <-> 4 <-> 5 <-> NULL
Reversed List: 5 <-> 4 <-> 3 <-> 2 <-> 1 <-> NULL

```
