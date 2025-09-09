# Develop a program to find articulation points (cut vertices) in a graph.

```c

#include <stdio.h>
#include <stdlib.h>

#define MAX 100

int graph[MAX][MAX], visited[MAX], disc[MAX], low[MAX], parent[MAX], ap[MAX];
int V, timeDFS = 0;

void articulationUtil(int u) {
    int children = 0;
    visited[u] = 1;
    disc[u] = low[u] = ++timeDFS;

    for (int v = 0; v < V; v++) {
        if (graph[u][v]) {
            if (!visited[v]) {
                children++;
                parent[v] = u;
                articulationUtil(v);

                if (low[v] < low[u])
                    low[u] = low[v];

                // Case 1: root of DFS tree with 2+ children
                if (parent[u] == -1 && children > 1)
                    ap[u] = 1;

                // Case 2: not root, check articulation condition
                if (parent[u] != -1 && low[v] >= disc[u])
                    ap[u] = 1;
            }
            else if (v != parent[u]) {
                if (disc[v] < low[u])
                    low[u] = disc[v];
            }
        }
    }
}

void findArticulationPoints() {
    for (int i = 0; i < V; i++) {
        visited[i] = 0;
        parent[i] = -1;
        ap[i] = 0;
    }

    for (int i = 0; i < V; i++) {
        if (!visited[i])
            articulationUtil(i);
    }

    printf("Articulation Points in the graph:\n");
    for (int i = 0; i < V; i++) {
        if (ap[i])
            printf("%d\n", i);
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
        graph[u][v] = graph[v][u] = 1; // Undirected graph
    }

    findArticulationPoints();
    return 0;
}


```

## Example Run:

- Input:

```c
Enter number of vertices: 5
Enter number of edges: 5
1 0
0 2
2 1
0 3
3 4
```

- Output:

```c
Articulation Points in the graph:
0
3
```
