# Implement a program to detect a cycle in a Singly Linked List.


## Concept:

- Use Floyd's Cycle Detection Algorithm (Tortoise and Hare).
- Maintain two pointers: slow and fast.
- Move slow by 1 step and fast by 2 steps.
- If they meet, a cycle exists.
- If fast reaches NULL, no cycle exists.

```c

#include <stdio.h>
#include <stdlib.h>

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

// Function to detect cycle in linked list
int detectCycle(struct Node* head) {
    struct Node* slow = head;
    struct Node* fast = head;

    while (fast != NULL && fast->next != NULL) {
        slow = slow->next;          // move slow by 1
        fast = fast->next->next;    // move fast by 2

        if (slow == fast) {
            return 1; // Cycle detected
        }
    }
    return 0; // No cycle
}

// Function to print the list (used only when no cycle exists)
void printList(struct Node* head, int limit) {
    struct Node* temp = head;
    int count = 0;
    printf("Linked List: ");
    while (temp != NULL && count < limit) {
        printf("%d -> ", temp->data);
        temp = temp->next;
        count++;
    }
    printf("NULL\n");
}

int main() {
    struct Node* head = NULL;

    // Create linked list: 10 -> 20 -> 30 -> 40 -> 50
    insertAtEnd(&head, 10);
    insertAtEnd(&head, 20);
    insertAtEnd(&head, 30);
    insertAtEnd(&head, 40);
    insertAtEnd(&head, 50);

    // Print list (no cycle case)
    printList(head, 10);

    // Case 1: No cycle
    if (detectCycle(head))
        printf("Cycle detected!\n");
    else
        printf("No cycle detected.\n");

    // Case 2: Create a cycle manually (last node points to second node)
    head->next->next->next->next->next = head->next; 

    if (detectCycle(head))
        printf("Cycle detected!\n");
    else
        printf("No cycle detected.\n");

    return 0;
}

```

### Sample Output:

```c
Linked List: 10 -> 20 -> 30 -> 40 -> 50 -> NULL
No cycle detected.
Cycle detected!
```
