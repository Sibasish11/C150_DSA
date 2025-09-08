# Implement a program to find the number of connected components in an undirected graph.

```c

#include <stdio.h>
#include <stdlib.h>

#define MAX 100

int adj[MAX][MAX];   // adjacency matrix
int visited[MAX];
int n; // number of vertices

// DFS function
void dfs(int v) {
    visited[v] = 1;
    for (int i = 0; i < n; i++) {
        if (adj[v][i] == 1 && !visited[i]) {
            dfs(i);
        }
    }
}

// Function to count connected components
int countConnectedComponents() {
    int count = 0;
    for (int i = 0; i < n; i++) {
        if (!visited[i]) {
            dfs(i);
            count++;
        }
    }
    return count;
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

    // Count components
    int components = countConnectedComponents();
    printf("Number of Connected Components: %d\n", components);

    return 0;
}

```

## Example Run:

### Input:

```c

Enter number of vertices: 6
Enter number of edges: 3
Enter edges (u v):
0 1
1 2
3 4

```

### Output:

```c

Number of Connected Components: 3

```

- (Components are {0,1,2}, {3,4}, {5})
