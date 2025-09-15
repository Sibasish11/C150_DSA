# Implement a program for Bucket Sort or Counting Sort for specific data ranges.

```c

class Solution {
    public static void countingSort(int[] arr, int maxVal) {
        int n = arr.length;
        int[] count = new int[maxVal + 1];  // frequency array

        // Step 1: Count frequencies
        for (int num : arr) {
            count[num]++;
        }

        // Step 2: Build sorted array
        int idx = 0;
        for (int i = 0; i <= maxVal; i++) {
            while (count[i] > 0) {
                arr[idx++] = i;
                count[i]--;
            }
        }
    }

    public static void main(String[] args) {
        int[] arr = {4, 2, 2, 8, 3, 3, 1};
        int maxVal = 8; // max element in array (range is 0–8)

        countingSort(arr, maxVal);

        System.out.print("Sorted Array: ");
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }
}


```

## Example

- Input:

```c
arr = [4, 2, 2, 8, 3, 3, 1]
```

### Steps:

- Count frequencies → [0, 1, 2, 2, 1, 0, 0, 0, 1] (for numbers 0 to 8).

- Build sorted array → [1, 2, 2, 3, 3, 4, 8].

### Output:

```c

[1, 2, 2, 3, 3, 4, 8]

```
