# Develop a program to rotate an array to the left by k positions.


## Concept:

- Left rotation means shifting each element of the array 
  to the left by 'k' steps.
- The first element moves to the end after one rotation.

### Example:

Input: arr[] = {1, 2, 3, 4, 5}, k = 2
Output: arr[] = {3, 4, 5, 1, 2}


## Approach:

1) Normalize k -> k = k % n (to avoid unnecessary rotations)
2) Store first k elements in a temporary array
3) Shift remaining (n-k) elements to the left
4) Copy temp[] elements at the end

```c

#include <stdio.h>

// Function to left rotate an array by k positions
void leftRotate(int arr[], int n, int k) {
    k = k % n; // Handle case when k > n

    int temp[k]; // Temporary array to store first k elements
    for (int i = 0; i < k; i++) {
        temp[i] = arr[i];
    }

    // Shift remaining elements to the left
    for (int i = 0; i < n - k; i++) {
        arr[i] = arr[i + k];
    }

    // Copy temp[] elements at the end
    for (int i = 0; i < k; i++) {
        arr[n - k + i] = temp[i];
    }
}

// Function to print array
void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");
}

int main() {
    int n, k;

    printf("Enter size of array: ");
    scanf("%d", &n);

    int arr[n];
    printf("Enter %d elements: ", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    printf("Enter number of rotations (k): ");
    scanf("%d", &k);

    printf("Original Array: ");
    printArray(arr, n);

    leftRotate(arr, n, k);

    printf("Array after %d left rotations: ", k);
    printArray(arr, n);

    return 0;
}

```

Sample Run:

```c
Enter size of array: 5
Enter 5 elements: 1 2 3 4 5
Enter number of rotations (k): 2

Original Array: 1 2 3 4 5
Array after 2 left rotations: 3 4 5 1 2

````
