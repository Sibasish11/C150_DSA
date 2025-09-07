# Implement a graph using an adjacency matrix representation. Include functions to add edges and print the graph.

```c

#include <stdio.h>
#include <stdlib.h>

// Graph structure using adjacency matrix 
struct Graph {
    int V;       // Number of vertices
    int** matrix; // 2D array for adjacency matrix
};

// Create a graph with V vertices
struct Graph* createGraph(int V) {
    struct Graph* graph = (struct Graph*)malloc(sizeof(struct Graph));
    graph->V = V;

    // Allocate memory for matrix
    graph->matrix = (int**)malloc(V * sizeof(int*));
    for (int i = 0; i < V; i++) {
        graph->matrix[i] = (int*)malloc(V * sizeof(int));
        for (int j = 0; j < V; j++)
            graph->matrix[i][j] = 0; // Initialize with 0
    }

    return graph;
}

// Add edge to an undirected graph
void addEdge(struct Graph* graph, int src, int dest) {
    graph->matrix[src][dest] = 1;
    graph->matrix[dest][src] = 1; // Comment this line for directed graph
}

// Print adjacency matrix
void printGraph(struct Graph* graph) {
    printf("Adjacency Matrix:\n");
    for (int i = 0; i < graph->V; i++) {
        for (int j = 0; j < graph->V; j++) {
            printf("%d ", graph->matrix[i][j]);
        }
        printf("\n");
    }
}

int main() {
    /*
        Example Graph (Undirected):
            0 -- 1
            |  / |
            | /  |
            2 -- 3
    */

    int V = 4;
    struct Graph* graph = createGraph(V);

    addEdge(graph, 0, 1);
    addEdge(graph, 0, 2);
    addEdge(graph, 1, 2);
    addEdge(graph, 1, 3);
    addEdge(graph, 2, 3);

    printGraph(graph);

    return 0;
}


```

## Example Output:

```c

Adjacency Matrix:
0 1 1 0 
1 0 1 1 
1 1 0 1 
0 1 1 0 

```
