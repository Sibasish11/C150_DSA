# Write a program to remove duplicates from an unsorted Singly Linked List.

```c

#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node* next;
};

// Function to create a new node
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

// Function to remove duplicates from unsorted list
void removeDuplicates(struct Node* head) {
    if (head == NULL) return;

    int hash[1000] = {0}; // assuming data values < 1000
    struct Node* current = head;
    struct Node* prev = NULL;

    while (current != NULL) {
        if (hash[current->data] == 1) {
            // Duplicate found -> delete node
            prev->next = current->next;
            free(current);
            current = prev->next;
        } else {
            // Mark this data as seen
            hash[current->data] = 1;
            prev = current;
            current = current->next;
        }
    }
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

    // Example: Linked List with duplicates
    insertEnd(&head, 4);
    insertEnd(&head, 2);
    insertEnd(&head, 4);
    insertEnd(&head, 3);
    insertEnd(&head, 2);
    insertEnd(&head, 1);

    printf("Original List: ");
    traverse(head);

    removeDuplicates(head);

    printf("After Removing Duplicates: ");
    traverse(head);

    return 0;
}


```

## Sample Output:

```c

Original List: 4 -> 2 -> 4 -> 3 -> 2 -> 1 -> NULL
After Removing Duplicates: 4 -> 2 -> 3 -> 1 -> NULL

```
