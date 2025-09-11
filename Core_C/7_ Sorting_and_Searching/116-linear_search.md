# Implement Linear Search to find an element in an array. Analyze its time complexity.

```c

#include <stdio.h>

// Function to perform Linear Search
int linearSearch(int arr[], int n, int key) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == key) {
            return i; // return index if found
        }
    }
    return -1; // not found
}

int main() {
    int arr[] = {10, 25, 30, 45, 50};
    int n = sizeof(arr) / sizeof(arr[0]);
    int key = 45;

    int result = linearSearch(arr, n, key);

    if (result != -1) {
        printf("Element %d found at index %d\n", key, result);
    } else {
        printf("Element %d not found in the array\n", key);
    }

    return 0;
}


```

## Example Output:

```c

Element 45 found at index 3

```
