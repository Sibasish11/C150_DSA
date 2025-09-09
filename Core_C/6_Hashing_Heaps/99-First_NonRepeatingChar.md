# Develop a program to find the first non-repeating character in a string using a Hash Map/Hash Table.

```c

#include <stdio.h>
#include <string.h>
#define CHAR_SIZE 256  // ASCII size

// Function to find first non-repeating character
char firstNonRepeatingChar(char *str) {
    int freq[CHAR_SIZE] = {0};

    // Step 1: Count frequency of each character
    for (int i = 0; str[i] != '\0'; i++) {
        freq[(unsigned char)str[i]]++;
    }

    // Step 2: Find first character with frequency 1
    for (int i = 0; str[i] != '\0'; i++) {
        if (freq[(unsigned char)str[i]] == 1) {
            return str[i];
        }
    }

    return '\0'; // No non-repeating character
}

int main() {
    char str[100];
    printf("Enter a string: ");
    fgets(str, sizeof(str), stdin);
    str[strcspn(str, "\n")] = '\0'; // remove newline

    char result = firstNonRepeatingChar(str);

    if (result != '\0')
        printf("First non-repeating character: %c\n", result);
    else
        printf("No non-repeating character found.\n");

    return 0;
}


```

## Example Run

- Input:

```c
Enter a string: programming
```

- Output:

```c
First non-repeating character: p
```

- Input:

```c
Enter a string: aabbcc
```

- Output:

```c
No non-repeating character found.
```
