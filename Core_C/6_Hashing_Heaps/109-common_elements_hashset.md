# Implement a program to find common elements in two arrays efficiently using a Hash Set.

```c

#include <stdio.h>
#include <stdbool.h>

#define MAX 1000 

void findCommon(int arr1[], int n1, int arr2[], int n2) {
    bool hash[MAX] = {false};
    bool printed[MAX] = {false}; // to avoid duplicate printing
    
    // Mark presence of elements in arr1
    for (int i = 0; i < n1; i++) {
        if (arr1[i] < MAX) {
            hash[arr1[i]] = true;
        }
    }
    
    printf("Common elements: ");
    for (int i = 0; i < n2; i++) {
        if (arr2[i] < MAX && hash[arr2[i]] && !printed[arr2[i]]) {
            printf("%d ", arr2[i]);
            printed[arr2[i]] = true; // mark printed to avoid duplicates
        }
    }
    printf("\n");
}

int main() {
    int arr1[] = {1, 5, 10, 20, 40, 80};
    int arr2[] = {6, 7, 20, 80, 100};
    
    int n1 = sizeof(arr1) / sizeof(arr1[0]);
    int n2 = sizeof(arr2) / sizeof(arr2[0]);
    
    findCommon(arr1, n1, arr2, n2);
    return 0;
}


```

## Example Run

- Input:

```c

arr1 = [1, 5, 10, 20, 40, 80]
arr2 = [6, 7, 20, 80, 100]

```

- Output:

```c

Common elements: [80, 20]

```
