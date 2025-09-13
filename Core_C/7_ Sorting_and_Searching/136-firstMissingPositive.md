# Develop a program to find the smallest missing positive integer in an unsorted array.

```c

#include <stdio.h>

void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Function to find smallest missing positive integer
int firstMissingPositive(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        while (arr[i] > 0 && arr[i] <= n && arr[arr[i] - 1] != arr[i]) {
            swap(&arr[i], &arr[arr[i] - 1]);
        }
    }

    for (int i = 0; i < n; i++) {
        if (arr[i] != i + 1)
            return i + 1;
    }
    return n + 1;
}

int main() {
    int arr[] = {3, 4, -1, 1};
    int n = sizeof(arr) / sizeof(arr[0]);

    int result = firstMissingPositive(arr, n);
    printf("The smallest missing positive integer is %d\n", result);

    return 0;
}


```

## Example Runs:

- Input:

```c

arr = [3, 4, -1, 1]

```

- Output:

```c

The smallest missing positive integer is 2

```

- Input:

```c

arr = [1, 2, 0]

```

- Output:

```c

The smallest missing positive integer is 3

```
