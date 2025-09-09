# Implement a program to find bridges (cut edges) in a graph.

```c

#include <stdio.h>
#include <stdlib.h>

#define MAX 100

int graph[MAX][MAX];
int visited[MAX], disc[MAX], low[MAX], parent[MAX];
int V, timeCounter;

void bridgeDFS(int u) {
    visited[u] = 1;
    disc[u] = low[u] = ++timeCounter;

    for (int v = 0; v < V; v++) {
        if (graph[u][v]) {
            if (!visited[v]) {
                parent[v] = u;
                bridgeDFS(v);

                // Update low[u]
                if (low[v] < low[u])
                    low[u] = low[v];

                // Bridge condition
                if (low[v] > disc[u])
                    printf("Bridge found: %d -- %d\n", u, v);
            }
            else if (v != parent[u]) {
                if (disc[v] < low[u])
                    low[u] = disc[v];
            }
        }
    }
}

void findBridges() {
    for (int i = 0; i < V; i++) {
        visited[i] = 0;
        parent[i] = -1;
    }

    timeCounter = 0;
    for (int i = 0; i < V; i++) {
        if (!visited[i])
            bridgeDFS(i);
    }
}

int main() {
    int E;
    printf("Enter number of vertices: ");
    scanf("%d", &V);

    printf("Enter number of edges: ");
    scanf("%d", &E);

    // Initialize adjacency matrix
    for (int i = 0; i < V; i++)
        for (int j = 0; j < V; j++)
            graph[i][j] = 0;

    printf("Enter edges (u v):\n");
    for (int i = 0; i < E; i++) {
        int u, v;
        scanf("%d %d", &u, &v);
        graph[u][v] = graph[v][u] = 1;  // Undirected graph
    }

    printf("Bridges in the graph:\n");
    findBridges();

    return 0;
}


```

## Example Run:

- Input

```c
Enter number of vertices: 5
Enter number of edges: 5
1 0
0 2
2 1
0 3
3 4
```

- Output

```c

Bridges in the graph:
3 - 4
0 - 3

```
