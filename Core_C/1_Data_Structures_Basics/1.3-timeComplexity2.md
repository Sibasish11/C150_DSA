# Write a program that demonstrates an O(N) time complexity operation (e.g., finding the maximum element in an array). Explain why it's O(N) in comments.

```java

#include <stdio.h>

int main() {
    int arr[] = {12, 45, 7, 89, 32, 56, 99, 23, 67};
    int n = sizeof(arr) / sizeof(arr[0]);
    
    int max = arr[0]; // Assume first element is max
    
    // Finding the maximum requires checking each element once
    // That means for N elements, we do N-1 comparisons
    // Time grows in direct proportion to N -> O(N)
    for (int i = 1; i < n; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    
    printf("Maximum element = %d\n", max);
    
    return 0;
}


```

## Output:

```java

Maximum element = 99


```
