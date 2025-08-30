# Develop a program to split a Singly Linked List into two halves.

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

// Function to split the linked list into two halves
void splitList(struct Node* head, struct Node** firstHalf, struct Node** secondHalf) {
    if (head == NULL || head->next == NULL) {
        *firstHalf = head;
        *secondHalf = NULL;
        return;
    }

    struct Node* slow = head;
    struct Node* fast = head->next;

    // Move fast by 2 steps and slow by 1 step
    while (fast != NULL && fast->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }

    // Split into two halves
    *firstHalf = head;
    *secondHalf = slow->next;
    slow->next = NULL; // Break the link
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
    struct Node* firstHalf = NULL;
    struct Node* secondHalf = NULL;

    // Example Linked List
    insertEnd(&head, 1);
    insertEnd(&head, 2);
    insertEnd(&head, 3);
    insertEnd(&head, 4);
    insertEnd(&head, 5);

    printf("Original List: ");
    traverse(head);

    splitList(head, &firstHalf, &secondHalf);

    printf("First Half: ");
    traverse(firstHalf);

    printf("Second Half: ");
    traverse(secondHalf);

    return 0;
}


```

# Sample Output:

```c

Original List: 1 -> 2 -> 3 -> 4 -> 5 -> NULL
First Half: 1 -> 2 -> 3 -> NULL
Second Half: 4 -> 5 -> NULL

```
