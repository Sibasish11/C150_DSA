# Develop a program to count the occurrences of an element in a sorted array using Binary Search.

```c

#include <stdio.h>

// Function to find the first occurrence of a key
int firstOccurrence(int arr[], int n, int key) {
    int low = 0, high = n - 1, result = -1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == key) {
            result = mid;
            high = mid - 1;  // move left
        }
        else if (arr[mid] < key)
            low = mid + 1;
        else
            high = mid - 1;
    }
    return result;
}

// Function to find the last occurrence of a key
int lastOccurrence(int arr[], int n, int key) {
    int low = 0, high = n - 1, result = -1;

    while (low <= high) {
        int mid = low + (high - low) / 2;

        if (arr[mid] == key) {
            result = mid;
            low = mid + 1;  // move right
        }
        else if (arr[mid] < key)
            low = mid + 1;
        else
            high = mid - 1;
    }
    return result;
}

// Function to count occurrences of a key
int countOccurrences(int arr[], int n, int key) {
    int first = firstOccurrence(arr, n, key);
    if (first == -1) return 0;  // element not found

    int last = lastOccurrence(arr, n, key);
    return (last - first + 1);
}

int main() {
    int arr[] = {1, 2, 4, 4, 4, 5, 6, 7};
    int n = sizeof(arr) / sizeof(arr[0]);
    int key = 4;

    int count = countOccurrences(arr, n, key);

    if (count > 0)
        printf("Element %d occurs %d times\n", key, count);
    else
        printf("Element %d not found in the array\n", key);

    return 0;
}


```

## Sample Output:

```c

Element 4 occurs 3 times

```
