# Write a program to check if a Singly Linked List is a palindrome.

```c

#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

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

// Insert a new node at the end
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

// Reverse a linked list
struct Node* reverseList(struct Node* head) {
    struct Node* prev = NULL;
    struct Node* curr = head;
    struct Node* nextNode;
    while (curr != NULL) {
        nextNode = curr->next;
        curr->next = prev;
        prev = curr;
        curr = nextNode;
    }
    return prev;
}

// Check if linked list is palindrome
bool isPalindrome(struct Node* head) {
    if (head == NULL || head->next == NULL) return true;

    // Step 1: Find middle (slow/fast pointer)
    struct Node* slow = head;
    struct Node* fast = head;
    while (fast->next != NULL && fast->next->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }

    // Step 2: Reverse second half
    struct Node* secondHalf = reverseList(slow->next);

    // Step 3: Compare both halves
    struct Node* p1 = head;
    struct Node* p2 = secondHalf;
    bool palindrome = true;
    while (p2 != NULL) {
        if (p1->data != p2->data) {
            palindrome = false;
            break;
        }
        p1 = p1->next;
        p2 = p2->next;
    }

    // (Optional) Restore original list
    slow->next = reverseList(secondHalf);

    return palindrome;
}

// Print the linked list
void traverse(struct Node* head) {
    while (head != NULL) {
        printf("%d -> ", head->data);
        head = head->next;
    }
    printf("NULL\n");
}

int main() {
    struct Node* head = NULL;

    // Example 1: Palindrome List: 1 -> 2 -> 3 -> 2 -> 1
    insertEnd(&head, 1);
    insertEnd(&head, 2);
    insertEnd(&head, 3);
    insertEnd(&head, 2);
    insertEnd(&head, 1);

    printf("Linked List: ");
    traverse(head);

    if (isPalindrome(head))
        printf("The linked list is a palindrome.\n");
    else
        printf("The linked list is NOT a palindrome.\n");

    return 0;
}

```

## Output:

```java

Linked List: 1 -> 2 -> 3 -> 2 -> 1 -> NULL
The linked list is a palindrome.

```

If we change the list to 1 -> 2 -> 3 -> 4, the output will be:

```java
Linked List: 1 -> 2 -> 3 -> 4 -> NULL
The linked list is NOT a palindrome.
```
