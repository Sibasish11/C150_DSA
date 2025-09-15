# Write a program to perform a permutation of an array based on a given permutation array.

```c

class Solution {
    public static int[] permuteArray(int[] arr, int[] perm) {
        int n = arr.length;
        int[] result = new int[n];

        for (int i = 0; i < n; i++) {
            result[perm[i]] = arr[i];
        }

        return result;
    }

    public static void main(String[] args) {
        int[] arr = {10, 20, 30, 40};
        int[] perm = {2, 0, 1, 3};

        int[] res = permuteArray(arr, perm);

        System.out.print("Permuted Array: ");
        for (int val : res) {
            System.out.print(val + " ");
        }
    }
}


```

## Example

- Input:

```c

arr  = [10, 20, 30, 40]
perm = [2, 0, 1, 3]

```

## Process:

```c

arr[0] = 10 should go to index 2.

arr[1] = 20 should go to index 0.

arr[2] = 30 should go to index 1.

arr[3] = 40 should go to index 3.

```

## Output:

```c

[20, 30, 10, 40]

```
