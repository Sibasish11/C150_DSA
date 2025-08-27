# Write a program to insert an element at a specific position in an array. Handle the case where the array is full.

```c

Explanation:

- An array has a fixed maximum size.
- To insert an element at a given position:
    1. Check if the array is already full.
    2. If not full, shift elements from the insertion position to the right.
    3. Place the new element at the specified position.
    4. Increase the array size by 1.


#include <stdio.h>
#define MAX_SIZE 100

// Function to insert an element into the array
void insertElement(int arr[], int *n, int pos, int value) {
    if (*n >= MAX_SIZE) {
        printf("Array is full! Cannot insert.\n");
        return;
    }
    if (pos < 0 || pos > *n) {
        printf("Invalid position! Must be between 0 and %d.\n", *n);
        return;
    }

    // Shift elements to the right
    for (int i = *n; i > pos; i--) {
        arr[i] = arr[i - 1];
    }

    // Insert the new element
    arr[pos] = value;
    (*n)++;

    printf("Element inserted successfully.\n");
}

void displayArray(int arr[], int n) {
    printf("Array: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int main() {
    int arr[MAX_SIZE], n, pos, value;

    printf("Enter number of elements (<= %d): ", MAX_SIZE);
    scanf("%d", &n);

    printf("Enter %d elements: ", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    printf("Enter position to insert (0 to %d): ", n);
    scanf("%d", &pos);

    printf("Enter value to insert: ");
    scanf("%d", &value);

    insertElement(arr, &n, pos, value);

    displayArray(arr, n);

    return 0;
}


```
