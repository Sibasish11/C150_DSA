# Write a program to demonstrate an O(log N) time complexity operation (e.g., repeatedly dividing a number by 2 until it reaches 1). Explain why it's O(log N) in comments.

```c

#include <stdio.h>

int main() {
    int n;

    printf("Enter a positive number: ");
    scanf("%d", &n);

    while (n > 1) {
        printf("%d\n", n);
        n = n / 2;
    }

    // Final output when n is 1
    printf("%d\n", n);

    return 0;
}
```

## Output:

```c
Enter a positive number: 20
20
10
5
2
1

```
