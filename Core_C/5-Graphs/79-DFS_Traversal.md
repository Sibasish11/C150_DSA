# Implement a program to perform a Depth-First Search (DFS) traversal on a graph starting from a given source node.

```c

#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

// Node for adjacency list 
struct Node {
    int dest;
    struct Node* next;
};

// Adjacency List 
struct AdjList {
    struct Node* head;
};

// Graph structure 
struct Graph {
    int V; // Number of vertices
    struct AdjList* array;
};

// Create a new adjacency list node
struct Node* createNode(int dest) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->dest = dest;
    newNode->next = NULL;
    return newNode;
}

// Create a graph with V vertices
struct Graph* createGraph(int V) {
    struct Graph* graph = (struct Graph*)malloc(sizeof(struct Graph));
    graph->V = V;
    graph->array = (struct AdjList*)malloc(V * sizeof(struct AdjList));

    for (int i = 0; i < V; i++)
        graph->array[i].head = NULL;

    return graph;
}

// Add edge (undirected graph)
void addEdge(struct Graph* graph, int src, int dest) {
    struct Node* newNode = createNode(dest);
    newNode->next = graph->array[src].head;
    graph->array[src].head = newNode;

    newNode = createNode(src);
    newNode->next = graph->array[dest].head;
    graph->array[dest].head = newNode;
}

// DFS Function (Recursive) 
void DFSUtil(struct Graph* graph, int v, bool visited[]) {
    visited[v] = true;
    printf("%d ", v);

    struct Node* temp = graph->array[v].head;
    while (temp) {
        if (!visited[temp->dest])
            DFSUtil(graph, temp->dest, visited);
        temp = temp->next;
    }
}

void DFS(struct Graph* graph, int start) {
    bool visited[graph->V];
    for (int i = 0; i < graph->V; i++)
        visited[i] = false;

    printf("DFS Traversal starting from vertex %d: ", start);
    DFSUtil(graph, start, visited);
    printf("\n");
}

int main() {
    /*
        Example Graph:
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

    DFS(graph, 0); // Start DFS from node 0

    return 0;
}


```

## Example Output:

```c

DFS Traversal starting from vertex 0: 0 2 3 1

```
