# Implement a program to pairwise swap nodes in a Singly Linked List.

```c

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = data;
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
}

struct Node* pairwiseSwap(struct Node* head) {
    if (head == NULL || head->next == NULL) return head;

    struct Node* prev = head;
    struct Node* curr = head->next;

    head = curr; // new head will be 2nd node

    while (1) {
        struct Node* next = curr->next;
        curr->next = prev;  // swap

        if (next == NULL || next->next == NULL) {
            prev->next = next;
            break;
        }

        prev->next = next->next;

        prev = next;
        curr = prev->next;
    }

    return head;
}

// Traverse and print
void traverse(struct Node* head) {
    while (head != NULL) {
        printf("%d -> ", head->data);
        head = head->next;
    }
    printf("NULL\n");
}

int main() {
    struct Node* head = NULL;

    // Example: Linked List
    insertEnd(&head, 1);
    insertEnd(&head, 2);
    insertEnd(&head, 3);
    insertEnd(&head, 4);
    insertEnd(&head, 5);

    printf("Original List: ");
    traverse(head);

    head = pairwiseSwap(head);

    printf("After Pairwise Swap: ");
    traverse(head);

    return 0;
}


```

## Sample Output:

```c
Original List: 1 -> 2 -> 3 -> 4 -> 5 -> NULL
After Pairwise Swap: 2 -> 1 -> 4 -> 3 -> 5 -> NULL
```
