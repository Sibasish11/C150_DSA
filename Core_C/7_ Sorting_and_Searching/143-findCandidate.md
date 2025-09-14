# Write a program to find the majority element in an array (appears more than n/2 times).

```c

#include <stdio.h>

// Function to find majority candidate using Boyer-Moore
int findCandidate(int arr[], int n) {
    int candidate = arr[0];
    int count = 1;

    for (int i = 1; i < n; i++) {
        if (arr[i] == candidate)
            count++;
        else
            count--;

        if (count == 0) {
            candidate = arr[i];
            count = 1;
        }
    }
    return candidate;
}

// Function to check if candidate is majority
int isMajority(int arr[], int n, int candidate) {
    int count = 0;
    for (int i = 0; i < n; i++) {
        if (arr[i] == candidate)
            count++;
    }
    return (count > n / 2);
}

int main() {
    int arr[] = {2, 2, 1, 1, 2, 2, 2};
    int n = sizeof(arr) / sizeof(arr[0]);

    int candidate = findCandidate(arr, n);

    if (isMajority(arr, n, candidate))
        printf("Majority element is %d\n", candidate);
    else
        printf("No majority element found\n");

    return 0;
}


```

##  Sample Output:

```c

Majority element is 2

```
