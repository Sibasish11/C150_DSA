# Write a program to reverse a Singly Linked List iteratively.

```c

#include <stdio.h>
#include <stdlib.h>

// Define a Node
struct Node {
    int data;
    struct Node* next;
};

// Function to print the linked list
void printList(struct Node* head) {
    struct Node* temp = head;
    printf("Linked List: ");
    while (temp != NULL) {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}

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

void reverseList(struct Node** head) {
    struct Node* prev = NULL;
    struct Node* current = *head;
    struct Node* next = NULL;

    while (current != NULL) {
        next = current->next;   // Save next
        current->next = prev;   // Reverse pointer
        prev = current;         // Move prev
        current = next;         // Move current
    }
    *head = prev;
}

int main() {
    struct Node* head = NULL;

    insertAtEnd(&head, 10);
    insertAtEnd(&head, 20);
    insertAtEnd(&head, 30);
    insertAtEnd(&head, 40);

    printf("Original List:\n");
    printList(head);

    // Reverse
    reverseList(&head);

    printf("Reversed List:\n");
    printList(head);

    return 0;
}

```

## Sample Output:

```c
Original List:
Linked List: 10 -> 20 -> 30 -> 40 -> NULL
Reversed List:
Linked List: 40 -> 30 -> 20 -> 10 -> NULL
```

```
