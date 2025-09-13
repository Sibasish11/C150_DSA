# Write a program to find pairs of elements in an array that sum up to a target value using a sorting-based approach.

```c

#include <stdio.h>
#include <stdlib.h>

// Compare function for qsort

int cmpfunc(const void *a, const void *b) {
    return (*(int*)a - *(int*)b);
}

// Function to find pairs with given sum
void findPairs(int arr[], int n, int target) {
    // Sort the array
    qsort(arr, n, sizeof(int), cmpfunc);

    int left = 0, right = n - 1;
    int found = 0;

    while (left < right) {
        int sum = arr[left] + arr[right];

        if (sum == target) {
            printf("Pair found: (%d, %d)\n", arr[left], arr[right]);
            found = 1;
            left++;
            right--;
        }
        else if (sum < target) {
            left++;
        }
        else {
            right--;
        }
    }

    if (!found) {
        printf("No pairs found with sum %d\n", target);
    }
}

int main() {
    int arr[] = {8, 7, 2, 5, 3, 1};
    int n = sizeof(arr) / sizeof(arr[0]);
    int target = 10;

    findPairs(arr, n, target);

    return 0;
}


```

## Example Run

- Input:

```c

arr = [8, 7, 2, 5, 3, 1]
target = 10

```

- Output:

```c

Pair found: (2, 8)
Pair found: (3, 7)

```
