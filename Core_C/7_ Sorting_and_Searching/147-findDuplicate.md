# Implement a program to find a duplicate element in an array of N+1 integers where elements are from 1 to N.

```c

#include <stdio.h>

// Function to find duplicate using Floyd's Cycle Detection
int findDuplicate(int arr[], int n) {
    int slow = arr[0];
    int fast = arr[0];

    // Phase 1: Detect cycle
    do {
        slow = arr[slow];
        fast = arr[arr[fast]];
    } while (slow != fast);

    // Phase 2: Find duplicate (entry point of cycle)
    slow = arr[0];
    while (slow != fast) {
        slow = arr[slow];
        fast = arr[fast];
    }

    return slow;
}

int main() {
    int arr[] = {3, 1, 3, 4, 2};  // N=4, size=5, duplicate=3
    int n = sizeof(arr) / sizeof(arr[0]) - 1; // N = size-1

    int duplicate = findDuplicate(arr, n);
    printf("Duplicate element: %d\n", duplicate);

    return 0;
}


```

## Sample Input:

```c

arr = [3, 1, 3, 4, 2]

```

## Sample Output:

```c

Duplicate element: 3

```
