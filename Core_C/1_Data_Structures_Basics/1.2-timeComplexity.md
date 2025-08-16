# Write a program that demonstrates an O(1) time complexity operation (e.g., accessing an element in an array by index). Explain why it's O(1) in comments.


```java

#include <stdio.h>

int main() {
    int arr[] = {10, 20, 30, 40, 50};
    int index = 3;  // We want to access the 4th element (index starts at 0)

    // Accessing an element by index is O(1)
    // Because the memory address of arr[index] is calculated directly:
    // address = base_address + (index * size_of_element)
    // This takes the same time regardless of the size of the array.
    printf("Element at index %d = %d\n", index, arr[index]);

    return 0;
}


```
