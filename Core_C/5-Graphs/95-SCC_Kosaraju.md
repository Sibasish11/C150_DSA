# Implement a program to find the strongly connected components (SCCs) in a directed graph (e.g., using Kosaraju's algorithm).

```c

#include <stdio.h>
#include <stdlib.h>

#define MAX 100

int V;
int graph[MAX][MAX], transpose[MAX][MAX];
int visited[MAX];
int stack[MAX], top = -1;

// Push onto stack
void push(int v) {
    stack[++top] = v;
}

// Pop from stack
int pop() {
    return stack[top--];
}

// DFS on original graph to fill finishing times
void dfs1(int v) {
    visited[v] = 1;
    for (int i = 0; i < V; i++) {
        if (graph[v][i] && !visited[i]) {
            dfs1(i);
        }
    }
    push(v);
}

// DFS on transposed graph
void dfs2(int v) {
    printf("%d ", v);
    visited[v] = 1;
    for (int i = 0; i < V; i++) {
        if (transpose[v][i] && !visited[i]) {
            dfs2(i);
        }
    }
}

int main() {
    int E;
    printf("Enter number of vertices: ");
    scanf("%d", &V);

    printf("Enter number of edges: ");
    scanf("%d", &E);

    // Initialize adjacency matrices
    for (int i = 0; i < V; i++)
        for (int j = 0; j < V; j++)
            graph[i][j] = transpose[i][j] = 0;

    printf("Enter directed edges (u v):\n");
    for (int i = 0; i < E; i++) {
        int u, v;
        scanf("%d %d", &u, &v);
        graph[u][v] = 1;         // Directed edge
        transpose[v][u] = 1;     // Reverse edge
    }

    // Step 1: Fill vertices in stack according to finishing times
    for (int i = 0; i < V; i++) visited[i] = 0;
    for (int i = 0; i < V; i++) {
        if (!visited[i]) dfs1(i);
    }

    // Step 2: Process all vertices in order defined by stack in transpose
    for (int i = 0; i < V; i++) visited[i] = 0;

    printf("\nStrongly Connected Components:\n");
    while (top != -1) {
        int v = pop();
        if (!visited[v]) {
            dfs2(v);
            printf("\n");
        }
    }

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

- Output:

```c

Strongly Connected Components:
0 2 1 
3 
4 

```
