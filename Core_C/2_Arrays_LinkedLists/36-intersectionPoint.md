# Implement a program to find the intersection point of two Singly Linked Lists.

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

// Function to get length of a linked list
int getLength(struct Node* head) {
    int count = 0;
    while (head != NULL) {
        count++;
        head = head->next;
    }
    return count;
}

// Function to find intersection point
struct Node* getIntersectionNode(struct Node* head1, struct Node* head2) {
    int len1 = getLength(head1);
    int len2 = getLength(head2);

    int diff = abs(len1 - len2);

    // Advance the longer list
    if (len1 > len2) {
        for (int i = 0; i < diff; i++) head1 = head1->next;
    } else {
        for (int i = 0; i < diff; i++) head2 = head2->next;
    }

    // Traverse both lists together until intersection is found
    while (head1 != NULL && head2 != NULL) {
        if (head1 == head2) return head1; // Intersection point
        head1 = head1->next;
        head2 = head2->next;
    }
    return NULL; // No intersection
}

// Function to print list
void printList(struct Node* head) {
    while (head != NULL) {
        printf("%d -> ", head->data);
        head = head->next;
    }
    printf("NULL\n");
}

int main() {
    /*
    Example:
    List 1: 10 -> 20 -> 30 \
                              -> 40 -> 50 -> NULL
    List 2:        15 ------/
    Intersection at node with data = 40
    */

    struct Node* common = createNode(40);
    common->next = createNode(50);

    // First linked list: 10 -> 20 -> 30 -> 40 -> 50
    struct Node* head1 = createNode(10);
    head1->next = createNode(20);
    head1->next->next = createNode(30);
    head1->next->next->next = common;

    // Second linked list: 15 -> 40 -> 50
    struct Node* head2 = createNode(15);
    head2->next = common;

    printf("List 1: ");
    printList(head1);
    printf("List 2: ");
    printList(head2);

    struct Node* intersection = getIntersectionNode(head1, head2);

    if (intersection != NULL)
        printf("Intersection point is: %d\n", intersection->data);
    else
        printf("No intersection found.\n");

    return 0;
}

```

## 📌 Sample Output:

```c

List 1: 10 -> 20 -> 30 -> 40 -> 50 -> NULL
List 2: 15 -> 40 -> 50 -> NULL
Intersection point is: 40

```
