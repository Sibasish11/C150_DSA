# Implement a graph using an adjacency list representation. Include functions to add edges and print the graph.

```c

#include <stdio.h>
#include <stdlib.h>

// Node structure for adjacency list 
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

    // Create an array of adjacency lists
    graph->array = (struct AdjList*)malloc(V * sizeof(struct AdjList));

    // Initialize each adjacency list as empty
    for (int i = 0; i < V; i++)
        graph->array[i].head = NULL;

    return graph;
}

// Add edge (undirected graph)
void addEdge(struct Graph* graph, int src, int dest) {
    // Add edge from src to dest
    struct Node* newNode = createNode(dest);
    newNode->next = graph->array[src].head;
    graph->array[src].head = newNode;

    // Since undirected, add edge from dest to src
    newNode = createNode(src);
    newNode->next = graph->array[dest].head;
    graph->array[dest].head = newNode;
}

// Print the graph
void printGraph(struct Graph* graph) {
    for (int v = 0; v < graph->V; v++) {
        struct Node* temp = graph->array[v].head;
        printf("Adjacency list of vertex %d: ", v);
        while (temp) {
            printf("-> %d ", temp->dest);
            temp = temp->next;
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

Adjacency list of vertex 0: -> 2 -> 1 
Adjacency list of vertex 1: -> 3 -> 2 -> 0 
Adjacency list of vertex 2: -> 3 -> 1 -> 0 
Adjacency list of vertex 3: -> 2 -> 1 

```
