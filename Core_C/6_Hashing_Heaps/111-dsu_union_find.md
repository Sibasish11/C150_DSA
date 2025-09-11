# Write a program to implement a simple disjoint set union (DSU) data structure with path compression and union by rank/size.

```c

#include <stdio.h>

#define MAX 100

int parent[MAX];
int rankArr[MAX];  // rank used to keep tree short

// Initialize DSU
void makeSet(int n) {
    for (int i = 0; i < n; i++) {
        parent[i] = i;   // each node is its own parent
        rankArr[i] = 0;  // rank starts as 0
    }
}

// Find with path compression
int find(int x) {
    if (parent[x] != x)
        parent[x] = find(parent[x]);  // path compression
    return parent[x];
}

// Union by rank
void unionSet(int x, int y) {
    int rootX = find(x);
    int rootY = find(y);

    if (rootX != rootY) {
        if (rankArr[rootX] < rankArr[rootY]) {
            parent[rootX] = rootY;
        } else if (rankArr[rootX] > rankArr[rootY]) {
            parent[rootY] = rootX;
        } else {
            parent[rootY] = rootX;
            rankArr[rootX]++;  // increase rank when equal
        }
    }
}

int main() {
    int n = 7;  // number of elements (0 to 6)
    makeSet(n);

    // Perform some unions
    unionSet(0, 1);
    unionSet(1, 2);
    unionSet(3, 4);
    unionSet(5, 6);
    unionSet(4, 5);

    // Test find operation
    printf("Find(2) = %d\n", find(2));
    printf("Find(6) = %d\n", find(6));

    // Check if two nodes are in the same set
    if (find(0) == find(2))
        printf("0 and 2 are in the same set\n");
    else
        printf("0 and 2 are in different sets\n");

    if (find(3) == find(6))
        printf("3 and 6 are in the same set\n");
    else
        printf("3 and 6 are in different sets\n");

    return 0;
}


```

## Example Output:

```rust

Find(2) = 0
Find(6) = 3
0 and 2 are in the same set
3 and 6 are in the same set

```
