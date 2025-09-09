# Write a program to find the shortest path in an unweighted graph (using BFS).

```c

#include <stdio.h>
#include <stdlib.h>

#define MAX 100

int graph[MAX][MAX]; // adjacency matrix
int visited[MAX], dist[MAX], parent[MAX];
int V;

void bfs(int src) {
    int queue[MAX], front = 0, rear = 0;

    for (int i = 0; i < V; i++) {
        visited[i] = 0;
        dist[i] = -1;   // -1 means unreachable
        parent[i] = -1;
    }

    visited[src] = 1;
    dist[src] = 0;
    queue[rear++] = src;

    while (front < rear) {
        int u = queue[front++];

        for (int v = 0; v < V; v++) {
            if (graph[u][v] && !visited[v]) {
                visited[v] = 1;
                dist[v] = dist[u] + 1;
                parent[v] = u;
                queue[rear++] = v;
            }
        }
    }
}

void printPath(int dest) {
    if (dist[dest] == -1) {
        printf("No path exists to node %d\n", dest);
        return;
    }

    printf("Shortest Path to %d (length = %d): ", dest, dist[dest]);

    int path[MAX], count = 0;
    for (int v = dest; v != -1; v = parent[v]) {
        path[count++] = v;
    }

    // Print in correct order
    for (int i = count - 1; i >= 0; i--) {
        printf("%d ", path[i]);
    }
    printf("\n");
}

int main() {
    int E, src;
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
        graph[u][v] = graph[v][u] = 1; // Undirected
    }

    printf("Enter source vertex: ");
    scanf("%d", &src);

    bfs(src);

    printf("\n--- Shortest Paths from %d ---\n", src);
    for (int i = 0; i < V; i++) {
        printPath(i);
    }

    return 0;
}


```

## Example Run:

- Input:

```c

Enter number of vertices: 6
Enter number of edges: 7
0 1
0 2
1 3
2 3
3 4
4 5
1 5
Enter source vertex: 0

```

- Output:

```c

--- Shortest Paths from 0 ---
Shortest Path to 0 (length = 0): 0
Shortest Path to 1 (length = 1): 0 1
Shortest Path to 2 (length = 1): 0 2
Shortest Path to 3 (length = 2): 0 1 3
Shortest Path to 4 (length = 3): 0 1 3 4
Shortest Path to 5 (length = 2): 0 1 5

```
