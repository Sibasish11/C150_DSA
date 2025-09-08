# Write a program to implement Topological Sort for a Directed Acyclic Graph (DAG) using Kahn's algorithm (BFS-based).

```c

#include <stdio.h>
#include <stdlib.h>

#define MAX 100

int adj[MAX][MAX];  // adjacency matrix
int n;              // number of vertices

// Function to perform Topological Sort using Kahn's Algorithm
void topologicalSort() {
    int inDegree[MAX] = {0};
    int queue[MAX], front = 0, rear = 0;
    int topoOrder[MAX], index = 0;

    // Step 1: Calculate in-degree for each vertex
    for (int u = 0; u < n; u++) {
        for (int v = 0; v < n; v++) {
            if (adj[u][v]) {
                inDegree[v]++;
            }
        }
    }

    // Step 2: Enqueue all vertices with in-degree = 0
    for (int i = 0; i < n; i++) {
        if (inDegree[i] == 0) {
            queue[rear++] = i;
        }
    }

    // Step 3: Process vertices
    while (front < rear) {
        int u = queue[front++];
        topoOrder[index++] = u;

        // Reduce in-degree of neighbors
        for (int v = 0; v < n; v++) {
            if (adj[u][v]) {
                inDegree[v]--;
                if (inDegree[v] == 0) {
                    queue[rear++] = v;
                }
            }
        }
    }

    // Step 4: Check if topological sort exists
    if (index != n) {
        printf("Graph has a cycle! Topological sort not possible.\n");
    } else {
        printf("Topological Order: ");
        for (int i = 0; i < index; i++) {
            printf("%d ", topoOrder[i]);
        }
        printf("\n");
    }
}

int main() {
    int edges, u, v;

    printf("Enter number of vertices: ");
    scanf("%d", &n);

    printf("Enter number of edges: ");
    scanf("%d", &edges);

    // Initialize adjacency matrix
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            adj[i][j] = 0;

    printf("Enter edges (u v) meaning u -> v:\n");
    for (int i = 0; i < edges; i++) {
        scanf("%d %d", &u, &v);
        adj[u][v] = 1; // Directed edge
    }

    topologicalSort();
    return 0;
}


```

## Example Run:

- Input

```c

Enter number of vertices: 6
Enter number of edges: 6
Enter edges (u v):
5 2
5 0
4 0
4 1
2 3
3 1

```

- Output:

```c

Topological Sort (Kahn's Algorithm): 4 5 2 3 1 0

```
