# Develop a program to check if a graph is bipartite using BFS.

```c

#include <stdio.h>
#include <stdlib.h>

#define MAX 100

int adj[MAX][MAX]; // adjacency matrix
int n; // number of vertices

// BFS function to check bipartite
int isBipartite(int src) {
    int color[MAX];
    for (int i = 0; i < n; i++) color[i] = -1; // -1 means uncolored

    int queue[MAX], front = 0, rear = 0;

    // Start with source vertex, assign color 0
    color[src] = 0;
    queue[rear++] = src;

    while (front < rear) {
        int u = queue[front++];

        for (int v = 0; v < n; v++) {
            if (adj[u][v]) {  // if edge exists
                if (color[v] == -1) { // uncolored, assign opposite color
                    color[v] = 1 - color[u];
                    queue[rear++] = v;
                } else if (color[v] == color[u]) {
                    return 0; // same color neighbor -> not bipartite
                }
            }
        }
    }
    return 1; // bipartite
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

    printf("Enter edges (u v):\n");
    for (int i = 0; i < edges; i++) {
        scanf("%d %d", &u, &v);
        adj[u][v] = adj[v][u] = 1; // Undirected graph
    }

    int result = isBipartite(0); // start BFS from vertex 0
    if (result)
        printf("The graph is Bipartite\n");
    else
        printf("The graph is NOT Bipartite\n");

    return 0;
}


```

## Example Run:

- Input:

```c

Enter number of vertices: 4
Enter number of edges: 4
Enter edges (u v):
0 1
1 2
2 3
3 0

```

## Output:

- The graph is Bipartite


### Input:

```c

Enter number of vertices: 3
Enter number of edges: 3
Enter edges (u v):
0 1
1 2
2 0

```

Output

```c

The graph is NOT Bipartite

```
