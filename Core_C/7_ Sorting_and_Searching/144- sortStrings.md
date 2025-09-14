# Implement a program to sort an array of strings alphabetically.

```c

#include <stdio.h>
#include <string.h>

#define MAX_STRINGS 100
#define MAX_LEN 100

// Function to sort strings using Bubble Sort
void sortStrings(char arr[][MAX_LEN], int n) {
    char temp[MAX_LEN];

    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (strcmp(arr[j], arr[j + 1]) > 0) {
                // Swap arr[j] and arr[j+1]
                strcpy(temp, arr[j]);
                strcpy(arr[j], arr[j + 1]);
                strcpy(arr[j + 1], temp);
            }
        }
    }
}

int main() {
    int n;
    char arr[MAX_STRINGS][MAX_LEN];

    printf("Enter number of strings: ");
    scanf("%d", &n);

    printf("Enter %d strings:\n", n);
    for (int i = 0; i < n; i++) {
        scanf("%s", arr[i]);  // reads a single word
    }

    sortStrings(arr, n);

    printf("\nSorted strings:\n");
    for (int i = 0; i < n; i++) {
        printf("%s\n", arr[i]);
    }

    return 0;
}


```

## Sample Input:

```c

Enter number of strings: 5
Enter 5 strings:
banana
apple
mango
cherry
grape

```

## Sample Output:

```c

Sorted strings:
apple
banana
cherry
grape
mango

```
