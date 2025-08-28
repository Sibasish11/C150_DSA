# Develop a program to remove the Nth node from the end of a Singly Linked List.

## Concept:

- Use two-pointer technique:
    1. Move 'first' pointer N steps ahead.
    2. Move 'first' and 'second' together until 'first' reaches NULL.
    3. Now 'second' points to the (N+1)th node from end, so we delete 'second->next'.
- Special case: If we need to delete the head itself.


```c

#include <stdio.h>
#include <stdlib.h>

// Define a Node
struct Node {
    int data;
    struct Node* next;
};

// Function to insert node at the end
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

// Function to print the list
void printList(struct Node* head) {
    struct Node* temp = head;
    printf("Linked List: ");
    while (temp != NULL) {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}

// Function to remove Nth node from end
void removeNthFromEnd(struct Node** head, int N) {
    struct Node* dummy = (struct Node*)malloc(sizeof(struct Node));
    dummy->next = *head;
    struct Node* first = dummy;
    struct Node* second = dummy;

    // Move 'first' ahead by N+1 steps
    for (int i = 0; i <= N; i++) {
        if (first == NULL) return; // N > length
        first = first->next;
    }

    // Move both pointers until 'first' reaches end
    while (first != NULL) {
        first = first->next;
        second = second->next;
    }

    // Delete node
    struct Node* temp = second->next;
    second->next = second->next->next;
    free(temp);

    *head = dummy->next;
    free(dummy);
}

int main() {
    struct Node* head = NULL;

    // Create linked list: 10 -> 20 -> 30 -> 40 -> 50
    insertAtEnd(&head, 10);
    insertAtEnd(&head, 20);
    insertAtEnd(&head, 30);
    insertAtEnd(&head, 40);
    insertAtEnd(&head, 50);

    printf("Original ");
    printList(head);

    // Remove 2nd node from end (40)
    removeNthFromEnd(&head, 2);

    printf("After removing 2nd node from end: ");
    printList(head);

    // Remove 4th node from end (10, head case)
    removeNthFromEnd(&head, 4);

    printf("After removing 4th node from end: ");
    printList(head);

    return 0;
}

```

## Sample Output:


```c

Original Linked List: 10 -> 20 -> 30 -> 40 -> 50 -> NULL
After removing 2nd node from end: 10 -> 20 -> 30 -> 50 -> NULL
After removing 4th node from end: 20 -> 30 -> 50 -> NULL

```
