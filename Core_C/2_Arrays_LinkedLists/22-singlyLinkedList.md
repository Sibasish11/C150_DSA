# Design and implement a Singly Linked List. Include functions for: 
- a) Insertion at the beginning. 
- b) Insertion at the end. 
- c) Insertion after a given node. 
- d) Deletion of a node by value. 
- e) Deletion of a node by position. 
- f) Traversal and printing all elements.

```c

#include <stdio.h>
#include <stdlib.h>


struct Node {
    int data;
    struct Node* next;
};

// Function to traverse and print the list
void printList(struct Node* head) {
    struct Node* temp = head;
    printf("Linked List: ");
    while (temp != NULL) {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}

// a) Insert at the beginning
void insertAtBeginning(struct Node** head, int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->next = *head;
    *head = newNode;
}

// b) Insert at the end
void insertAtEnd(struct Node** head, int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->next = NULL;

    if (*head == NULL) {
        *head = newNode;
        return;
    }

    struct Node* temp = *head;
    while (temp->next != NULL) {
        temp = temp->next;
    }
    temp->next = newNode;
}

// c) Insert after a given node
void insertAfter(struct Node* prevNode, int data) {
    if (prevNode == NULL) {
        printf("Previous node cannot be NULL\n");
        return;
    }
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
    newNode->next = prevNode->next;
    prevNode->next = newNode;
}

// d) Delete node by value
void deleteByValue(struct Node** head, int key) {
    struct Node* temp = *head;
    struct Node* prev = NULL;

    // If head node itself holds the key
    if (temp != NULL && temp->data == key) {
        *head = temp->next;
        free(temp);
        return;
    }

    // Search for the key
    while (temp != NULL && temp->data != key) {
        prev = temp;
        temp = temp->next;
    }

    // Key not found
    if (temp == NULL) return;

    prev->next = temp->next;
    free(temp);
}

// e) Delete node by position (0-based index)
void deleteByPosition(struct Node** head, int position) {
    if (*head == NULL) return;

    struct Node* temp = *head;

    // Delete head
    if (position == 0) {
        *head = temp->next;
        free(temp);
        return;
    }

    // Find previous node
    for (int i = 0; temp != NULL && i < position - 1; i++) {
        temp = temp->next;
    }

    // If position is out of range
    if (temp == NULL || temp->next == NULL) return;

    struct Node* next = temp->next->next;
    free(temp->next);
    temp->next = next;
}

int main() {
    struct Node* head = NULL;

    // Demonstration
    insertAtEnd(&head, 10);
    insertAtEnd(&head, 20);
    insertAtEnd(&head, 30);
    printList(head);  // 10 -> 20 -> 30

    insertAtBeginning(&head, 5);
    printList(head);  // 5 -> 10 -> 20 -> 30

    insertAfter(head->next, 15);  // After 10
    printList(head);  // 5 -> 10 -> 15 -> 20 -> 30

    deleteByValue(&head, 20);
    printList(head);  // 5 -> 10 -> 15 -> 30

    deleteByPosition(&head, 2); // Delete node at index 2 (15)
    printList(head);  // 5 -> 10 -> 30

    return 0;
}


```

## Sample Output:

```c
Linked List: 10 -> 20 -> 30 -> NULL
Linked List: 5 -> 10 -> 20 -> 30 -> NULL
Linked List: 5 -> 10 -> 15 -> 20 -> 30 -> NULL
Linked List: 5 -> 10 -> 15 -> 30 -> NULL
Linked List: 5 -> 10 -> 30 -> NULL
```
