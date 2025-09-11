# Implement a program to check if a given string is an anagram of another string using a hash map or frequency array.

```c

#include <stdio.h>
#include <string.h>
#include <stdbool.h>

#define CHAR_RANGE 256  

// Function to check if two strings are anagrams
bool areAnagrams(char str1[], char str2[]) {
    int count[CHAR_RANGE] = {0};

    // If lengths differ, they cannot be anagrams
    if (strlen(str1) != strlen(str2))
        return false;

    // Count frequency differences
    for (int i = 0; str1[i] && str2[i]; i++) {
        count[(unsigned char)str1[i]]++;
        count[(unsigned char)str2[i]]--;
    }

    // Check if all counts are zero
    for (int i = 0; i < CHAR_RANGE; i++) {
        if (count[i] != 0)
            return false;
    }

    return true;
}

int main() {
    char str1[] = "listen";
    char str2[] = "silent";

    if (areAnagrams(str1, str2))
        printf("\"%s\" and \"%s\" are Anagrams.\n", str1, str2);
    else
        printf("\"%s\" and \"%s\" are NOT Anagrams.\n", str1, str2);

    return 0;
}


```

## Example Output:

```c

"listen" and "silent" are Anagrams.

```
