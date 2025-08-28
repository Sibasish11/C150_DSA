# Implement a program to remove duplicate elements from a sorted array in-place.



## Concept:

- Since the array is sorted, duplicates will always be adjacent.
- We use the "two-pointer technique":
    - Keep one pointer `j` for the index of the unique array.
    - Traverse the array with another pointer `i`.
    - Whenever arr[i] != arr[j], increment j and copy arr[i] to arr[j].
- Finally, new array length will be j+1.
```c


#include <stdio.h>

// Function to remove duplicates in-place
int removeDuplicates(int arr[], int n) {
    if (n == 0 || n == 1) {
        return n; // No duplicates possible
    }

    int j = 0; 

    for (int i = 1; i < n; i++) {
        if (arr[i] != arr[j]) {
            j++;
            arr[j] = arr[i];
        }
    }

    return j + 1; 
}

int main() {
    int n;
    printf("Enter size of sorted array: ");
    scanf("%d", &n);

    int arr[n];
    printf("Enter %d sorted elements: ", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    int newSize = removeDuplicates(arr, n);

    printf("Array after removing duplicates: ");
    for (int i = 0; i < newSize; i++) {
        printf("%d ", arr[i]);
    }
    printf("\n");

    return 0;
}

```
## Sample Run 1:

```c
Enter size of sorted array: 10
Enter 10 sorted elements: 1 1 2 2 3 4 4 5 5 6
Array after removing duplicates: 1 2 3 4 5 6
```

## Sample Run 2:

```c
Enter size of sorted array: 5
Enter 5 sorted elements: 2 2 2 2 2
Array after removing duplicates: 2
```
