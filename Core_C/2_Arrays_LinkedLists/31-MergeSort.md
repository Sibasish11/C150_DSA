# Develop a program to sort a Singly Linked List (e.g., using Merge Sort adapted for linked lists).

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

// Split list into two halves
void splitList(struct Node* source, struct Node** front, struct Node** back) {
    struct Node* slow = source;
    struct Node* fast = source->next;

    // Move fast by 2 and slow by 1
    while (fast != NULL) {
        fast = fast->next;
        if (fast != NULL) {
            slow = slow->next;
            fast = fast->next;
        }
    }

    *front = source;
    *back = slow->next;
    slow->next = NULL;
}

// Merge two sorted lists
struct Node* mergeLists(struct Node* a, struct Node* b) {
    if (!a) return b;
    if (!b) return a;

    struct Node* result = NULL;
    if (a->data <= b->data) {
        result = a;
        result->next = mergeLists(a->next, b);
    } else {
        result = b;
        result->next = mergeLists(a, b->next);
    }
    return result;
}

// Merge Sort on linked list
void mergeSort(struct Node** headRef) {
    struct Node* head = *headRef;
    if (!head || !head->next) return;

    struct Node* a;
    struct Node* b;

    // Step 1: Split the list
    splitList(head, &a, &b);

    // Step 2: Sort both halves
    mergeSort(&a);
    mergeSort(&b);

    // Step 3: Merge sorted halves
    *headRef = mergeLists(a, b);
}

// Traverse and print
void traverse(struct Node* head) {
    while (head != NULL) {
        printf("%d -> ", head->data);
        head = head->next;
    }
    printf("NULL\n");
}

// Main function
int main() {
    struct Node* head = NULL;

    // Example: Unsorted Linked List
    insertEnd(&head, 5);
    insertEnd(&head, 2);
    insertEnd(&head, 8);
    insertEnd(&head, 1);
    insertEnd(&head, 3);

    printf("Original List: ");
    traverse(head);

    mergeSort(&head);

    printf("Sorted List: ");
    traverse(head);

    return 0;
}

```

## Sample Output:
```c
Original List: 5 -> 2 -> 8 -> 1 -> 3 -> NULL
Sorted List: 1 -> 2 -> 3 -> 5 -> 8 -> NULL
```

```
