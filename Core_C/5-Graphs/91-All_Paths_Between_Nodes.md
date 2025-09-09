# Write a program to find all paths between two given nodes in a graph.

```c

#include <stdio.h>
#include <stdlib.h>

#define MAX 100

int graph[MAX][MAX];
int visited[MAX];
int path[MAX];
int V;

void printPath(int path[], int pathLen) {
    for (int i = 0; i < pathLen; i++) {
        printf("%d ", path[i]);
    }
    printf("\n");
}

void dfsAllPaths(int u, int dest, int path[], int pathLen) {
    visited[u] = 1;
    path[pathLen] = u;
    pathLen++;

    if (u == dest) {
        printPath(path, pathLen);
    } else {
        for (int v = 0; v < V; v++) {
            if (graph[u][v] && !visited[v]) {
                dfsAllPaths(v, dest, path, pathLen);
            }
        }
    }

    // Backtrack
    pathLen--;
    visited[u] = 0;
}

int main() {
    int E, src, dest;
    printf("Enter number of vertices: ");
    scanf("%d", &V);

    printf("Enter number of edges: ");
    scanf("%d", &E);

    // Initialize graph
    for (int i = 0; i < V; i++)
        for (int j = 0; j < V; j++)
            graph[i][j] = 0;

    printf("Enter edges (u v):\n");
    for (int i = 0; i < E; i++) {
        int u, v;
        scanf("%d %d", &u, &v);
        graph[u][v] = 1;  // Directed graph
    }

    printf("Enter source and destination: ");
    scanf("%d %d", &src, &dest);

    for (int i = 0; i < V; i++) visited[i] = 0;

    printf("All paths from %d to %d:\n", src, dest);
    dfsAllPaths(src, dest, path, 0);

    return 0;
}


```

## Example Run:

### Input:

```c

Enter number of vertices: 4
Enter number of edges: 5
0 1
0 2
1 2
1 3
2 3
Enter source and destination: 0 3

```

## Output:

```c

All paths from 0 to 3:
0 1 2 3
0 1 3
0 2 3

```
