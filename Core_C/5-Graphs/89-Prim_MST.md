# Develop a program to find the Minimum Spanning Tree (MST) of a graph using Prim's algorithm.

```c

#include <stdio.h>
#include <limits.h>

#define MAX 100

int n;                
int graph[MAX][MAX];   // Adjacency matrix

// Find vertex with minimum key value not yet in MST
int minKey(int key[], int mstSet[]) {
    int min = INT_MAX, min_index;

    for (int v = 0; v < n; v++) {
        if (mstSet[v] == 0 && key[v] < min) {
            min = key[v];
            min_index = v;
        }
    }
    return min_index;
}

// Print MST result
void printMST(int parent[], int graph[MAX][MAX]) {
    int totalWeight = 0;
    printf("Edge   Weight\n");
    for (int i = 1; i < n; i++) {
        printf("%d - %d    %d\n", parent[i], i, graph[i][parent[i]]);
        totalWeight += graph[i][parent[i]];
    }
    printf("Total weight of MST = %d\n", totalWeight);
}

// Prim's Algorithm
void primMST() {
    int parent[MAX];   // Store MST
    int key[MAX];      // Key values
    int mstSet[MAX];   // To represent set of vertices in MST

    // Initialize all keys as infinite
    for (int i = 0; i < n; i++) {
        key[i] = INT_MAX;
        mstSet[i] = 0;
    }

    // Start from vertex 0
    key[0] = 0;
    parent[0] = -1;

    // Build MST
    for (int count = 0; count < n - 1; count++) {
        int u = minKey(key, mstSet); // Pick min key vertex
        mstSet[u] = 1;

        // Update key values of adjacent vertices
        for (int v = 0; v < n; v++) {
            if (graph[u][v] && mstSet[v] == 0 && graph[u][v] < key[v]) {
                parent[v] = u;
                key[v] = graph[u][v];
            }
        }
    }

    printMST(parent, graph);
}

int main() {
    int edges, u, v, w;

    printf("Enter number of vertices: ");
    scanf("%d", &n);

    // Initialize adjacency matrix
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            graph[i][j] = 0;

    printf("Enter number of edges: ");
    scanf("%d", &edges);

    printf("Enter edges (u v w):\n");
    for (int i = 0; i < edges; i++) {
        scanf("%d %d %d", &u, &v, &w);
        graph[u][v] = w;
        graph[v][u] = w;  // Undirected graph
    }

    primMST();

    return 0;
}


```

## Example Run

### Input:

```typescript

Enter number of vertices: 5
Enter number of edges: 7
0 1 2
0 3 6
1 2 3
1 3 8
1 4 5
2 4 7
3 4 9

```

### Output:

```c

Edge   Weight
0 - 1    2
1 - 2    3
1 - 4    5
0 - 3    6
Total weight of MST: 16

```
