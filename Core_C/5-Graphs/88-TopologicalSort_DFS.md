# Implement a program to implement Topological Sort for a Directed Acyclic Graph (DAG) using DFS.

```c

#include <stdio.h>
#include <stdlib.h>

#define MAX 100

int adj[MAX][MAX];  // adjacency matrix
int visited[MAX]; 
int stack[MAX];     
int top = -1;       // stack pointer
int n;           

// Push element into stack
void push(int v) {
    stack[++top] = v;
}

// Pop and print stack elements (Topological Order)
void printStack() {
    printf("Topological Sort (DFS-based): ");
    while (top != -1) {
        printf("%d ", stack[top--]);
    }
    printf("\n");
}

// DFS function
void dfs(int v) {
    visited[v] = 1;

    // Explore all adjacent vertices
    for (int i = 0; i < n; i++) {
        if (adj[v][i] && !visited[i]) {
            dfs(i);
        }
    }

    // After visiting all neighbors, push this node into stack
    push(v);
}

void topologicalSort() {
    // Mark all vertices unvisited
    for (int i = 0; i < n; i++) {
        visited[i] = 0;
    }

    // Call DFS for unvisited vertices
    for (int i = 0; i < n; i++) {
        if (!visited[i])
            dfs(i);
    }

    // Print result
    printStack();
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

    printf("Enter edges (u v) for Directed Graph:\n");
    for (int i = 0; i < edges; i++) {
        scanf("%d %d", &u, &v);
        adj[u][v] = 1;  // Directed edge u → v
    }

    topologicalSort();

    return 0;
}


```

## Example Run:

### Input:

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

### Output:

```c
Topological Sort (DFS-based): 5 4 2 3 1 0
```
