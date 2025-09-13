# Implement a program to find triplets in an array that sum up to a target value.

```c

#include <stdio.h>
#include <stdlib.h>

int cmpfunc(const void *a, const void *b) {
    return (*(int*)a - *(int*)b);
}

// Function to find triplets with given sum
void findTriplets(int arr[], int n, int target) {
    // Sort the array
    qsort(arr, n, sizeof(int), cmpfunc);

    int found = 0;

    for (int i = 0; i < n - 2; i++) {
        int left = i + 1, right = n - 1;

        while (left < right) {
            int sum = arr[i] + arr[left] + arr[right];

            if (sum == target) {
                printf("Triplet found: (%d, %d, %d)\n", arr[i], arr[left], arr[right]);
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
    }

    if (!found) {
        printf("No triplets found with sum %d\n", target);
    }
}

int main() {
    int arr[] = {12, 3, 4, 1, 6, 9};
    int n = sizeof(arr) / sizeof(arr[0]);
    int target = 24;

    findTriplets(arr, n, target);

    return 0;
}


```

## Example Run:

- Input:

```c

arr = [12, 3, 4, 1, 6, 9]
target = 24

```

- Output:

```c

Triplet found: (3, 9, 12)
Triplet found: (4, 9, 11)  // if 11 existed

```
