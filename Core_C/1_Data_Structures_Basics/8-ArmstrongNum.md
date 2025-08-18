# Write a program to check if a given number is an Armstrong number. Analyze its time complexity based on the number of digits.

Program: Armstrong Number Checker
---------------------------------
An Armstrong number (also known as a narcissistic number) is a number 
that is equal to the sum of its own digits each raised to the power 
of the number of digits.

Example:
--------
153 = 1^3 + 5^3 + 3^3 = 153  → Armstrong
9474 = 9^4 + 4^4 + 7^4 + 4^4 = 9474 → Armstrong
123 is not an Armstrong number.

Algorithm:
----------
1. Count the number of digits (d) in the number N.
2. For each digit, compute digit^d and accumulate the sum.
3. If the sum equals the original number → Armstrong.

Time Complexity Analysis:
-------------------------
- Let d = number of digits in the number.
- Step 1: Counting digits → O(d).
- Step 2: Computing digit^d for each digit → O(d).
- Total Time Complexity = O(d)
- Space Complexity = O(1) (only a few variables used).

```c

#include <stdio.h>
#include <math.h>

// Function to check if a number is Armstrong
int isArmstrong(int n) {
    int original = n, sum = 0, digits = 0;

    // Step 1: Count digits
    int temp = n;
    while (temp > 0) {
        digits++;
        temp /= 10;
    }

    // Step 2: Calculate sum of powers of digits
    temp = n;
    while (temp > 0) {
        int digit = temp % 10;
        sum += (int)pow(digit, digits);
        temp /= 10;
    }

    // Step 3: Check condition
    return (sum == original);
}

int main() {
    int n;
    printf("Enter a number: ");
    scanf("%d", &n);

    if (isArmstrong(n))
        printf("%d is an Armstrong number.\n", n);
    else
        printf("%d is NOT an Armstrong number.\n", n);

    return 0;
}

```

## Output:

```c

Input: 153
Output: 153 is an Armstrong number.

Input: 9474
Output: 9474 is an Armstrong number.

Input: 123
Output: 123 is NOT an Armstrong number.


```
