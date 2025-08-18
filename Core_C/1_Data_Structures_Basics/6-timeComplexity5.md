# Write a program to calculate the Nth Fibonacci number using a recursive approach. Analyze and comment on its exponential time complexity (O(2^N)).

```java

#include <stdio.h>

int fibonacci(int n) {
    if (n == 0) return 0;  // Base case
    if (n == 1) return 1;  // Base case
    return fibonacci(n - 1) + fibonacci(n - 2);
}

int main() {
    int n;
    printf("Enter the value of n: ");
    scanf("%d", &n);

    printf("Fibonacci number at position %d is: %d\n", n, fibonacci(n));
    return 0;
}


```

## ⚡ Example for n = 5:

f(5)
= f(4) + f(3)
= (f(3) + f(2)) + (f(2) + f(1))
= ((f(2) + f(1)) + (f(1) + f(0))) + ((f(1) + f(0)) + 1)


You can see many repeated calls like f(2), f(1) → causes exponential blowup.

Case 1: Input n = 5
```java
Enter the value of n: 5
Fibonacci number at position 5 is: 5
```

Explanation: Fibonacci sequence is
```java
0, 1, 1, 2, 3, 5, 8, 13...
So the 5th Fibonacci number (if counting from 0) is 5.
```
Case 2: Input n = 7
```java
Enter the value of n: 7
Fibonacci number at position 7 is: 13
```

Sequence: 0, 1, 1, 2, 3, 5, 8, 13 → at position 7 → 13.

Case 3: Input n = 10
```java
Enter the value of n: 10
Fibonacci number at position 10 is: 55
```

Sequence up to 10: 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55.
