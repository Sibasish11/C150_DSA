# Implement a program to merge two sorted Singly Linked Lists into a single sorted list.

## Concept:
- Both lists are already sorted.
- Use a dummy node and tail pointer to build the merged list.
- Compare current nodes of both lists and attach the smaller one.
- Continue until one list is exhausted, then attach the other list.

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

// Insert at end (helper to build list)
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

// Traverse list
void traverse(struct Node* head) {
    while (head != NULL) {
        printf("%d -> ", head->data);
        head = head->next;
    }
    printf("NULL\n");
}

// Merge two sorted lists
struct Node* mergeSortedLists(struct Node* l1, struct Node* l2) {
    // Dummy node to simplify code
    struct Node dummy;
    struct Node* tail = &dummy;
    dummy.next = NULL;

    while (l1 != NULL && l2 != NULL) {
        if (l1->data <= l2->data) {
            tail->next = l1;
            l1 = l1->next;
        } else {
            tail->next = l2;
            l2 = l2->next;
        }
        tail = tail->next;
    }

    // Attach remaining nodes
    if (l1 != NULL) tail->next = l1;
    if (l2 != NULL) tail->next = l2;

    return dummy.next;
}

// Main
int main() {
    struct Node* list1 = NULL;
    struct Node* list2 = NULL;

    // List 1: 1 -> 3 -> 5
    insertEnd(&list1, 1);
    insertEnd(&list1, 3);
    insertEnd(&list1, 5);

    // List 2: 2 -> 4 -> 6 -> 8
    insertEnd(&list2, 2);
    insertEnd(&list2, 4);
    insertEnd(&list2, 6);
    insertEnd(&list2, 8);

    printf("List 1: ");
    traverse(list1);
    printf("List 2: ");
    traverse(list2);

    struct Node* mergedList = mergeSortedLists(list1, list2);

    printf("\nMerged Sorted List: ");
    traverse(mergedList);

    return 0;
}

```

## Sample Output:

```c

List 1: 1 -> 3 -> 5 -> NULL
List 2: 2 -> 4 -> 6 -> 8 -> NULL

Merged Sorted List: 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 8 -> NULL

```
