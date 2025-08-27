# Implement a program to delete an element from a specific position in an array.

```c

Explanation:

- To delete an element at a given position in an array:
    1. Check if the position is valid (0 ≤ pos < current size).
    2. Shift all elements from pos+1 to the left by one index.
    3. Reduce the size of the array by 1.


#include <stdio.h>
#define MAX_SIZE 100

// Function to delete an element from the array
void deleteElement(int arr[], int *n, int pos) {
    if (*n <= 0) {
        printf("Array is empty! Cannot delete.\n");
        return;
    }
    if (pos < 0 || pos >= *n) {
        printf("Invalid position! Must be between 0 and %d.\n", *n - 1);
        return;
    }

    // Shift elements to the left
    for (int i = pos; i < *n - 1; i++) {
        arr[i] = arr[i + 1];
    }

    (*n)--; // Decrease array size
    printf("Element deleted successfully.\n");
}

// Function to display the array
void displayArray(int arr[], int n) {
    printf("Array: ");
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int main() {
    int arr[MAX_SIZE], n, pos;

    printf("Enter number of elements (<= %d): ", MAX_SIZE);
    scanf("%d", &n);

    printf("Enter %d elements: ", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    printf("Enter position to delete (0 to %d): ", n - 1);
    scanf("%d", &pos);

    deleteElement(arr, &n, pos);

    displayArray(arr, n);

    return 0;
}


```


## ✅ Example Run:
```c
Enter number of elements (<= 100): 5
Enter 5 elements: 10 20 30 40 50
Enter position to delete (0 to 4): 2
Element deleted successfully.
Array: 10 20 40 50
```

## If you enter an invalid position:

Invalid position! Must be between 0 and 4.
