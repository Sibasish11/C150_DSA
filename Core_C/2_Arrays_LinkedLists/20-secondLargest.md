# Write a program to find the second largest element in an unsorted array.

## Concept:

- We need to scan the array to determine the largest and 
  second largest elements.
- We will keep track of two variables:
    1. largest
    2. secondLargest
- While traversing the array:
    - If arr[i] > largest:
         secondLargest = largest
         largest = arr[i]
    - Else if arr[i] < largest && arr[i] > secondLargest:
         secondLargest = arr[i]

Edge Cases:

1) If the array has fewer than 2 distinct elements, 
   then "second largest does not exist".
2) Works for arrays with duplicates.

```java


#include <stdio.h>
#include <limits.h>  // for INT_MIN

int findSecondLargest(int arr[], int n) {
    if (n < 2) {
        printf("Array must have at least two elements.\n");
        return -1;
    }

    int largest = INT_MIN, secondLargest = INT_MIN;

    for (int i = 0; i < n; i++) {
        if (arr[i] > largest) {
            secondLargest = largest;
            largest = arr[i];
        }
        else if (arr[i] > secondLargest && arr[i] < largest) {
            secondLargest = arr[i];
        }
    }

    if (secondLargest == INT_MIN) {
        printf("No second largest element (all elements may be equal).\n");
        return -1;
    }

    return secondLargest;
}

int main() {
    int n;
    printf("Enter size of array: ");
    scanf("%d", &n);

    int arr[n];
    printf("Enter %d elements: ", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &arr[i]);
    }

    int result = findSecondLargest(arr, n);

    if (result != -1) {
        printf("The second largest element is: %d\n", result);
    }

    return 0;
}
```

## Sample Run 1:

```java

Enter size of array: 6
Enter 6 elements: 10 20 4 45 99 45
The second largest element is: 45

```

## Sample Run 2:
```java
Enter size of array: 4
Enter 4 elements: 7 7 7 7
No second largest element (all elements may be equal).
```
