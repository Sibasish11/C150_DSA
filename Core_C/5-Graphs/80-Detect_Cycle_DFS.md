# Develop a program to detect a cycle in an undirected graph using DFS.

```c

#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

// Node for adjacency list 
struct Node {
    int dest;
    struct Node* next;
};

//  Adjacency List 
struct AdjList {
    struct Node* head;
};

// Graph structure 
struct Graph {
    int V;
    struct AdjList* array;
};

// Create a new adjacency list node
struct Node* createNode(int dest) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->dest = dest;
    newNode->next = NULL;
    return newNode;
}

// Create a graph
struct Graph* createGraph(int V) {
    struct Graph* graph = (struct Graph*)malloc(sizeof(struct Graph));
    graph->V = V;
    graph->array = (struct AdjList*)malloc(V * sizeof(struct AdjList));

    for (int i = 0; i < V; i++)
        graph->array[i].head = NULL;

    return graph;
}

// Add an edge (undirected graph)
void addEdge(struct Graph* graph, int src, int dest) {
    struct Node* newNode = createNode(dest);
    newNode->next = graph->array[src].head;
    graph->array[src].head = newNode;

    newNode = createNode(src);
    newNode->next = graph->array[dest].head;
    graph->array[dest].head = newNode;
}

// DFS Utility to detect cycle 
bool DFSUtil(struct Graph* graph, int v, bool visited[], int parent) {
    visited[v] = true;

    struct Node* temp = graph->array[v].head;
    while (temp) {
        int u = temp->dest;

        if (!visited[u]) {
            if (DFSUtil(graph, u, visited, v))
                return true;
        }
        // If visited and not parent -> cycle
        else if (u != parent) {
            return true;
        }
        temp = temp->next;
    }
    return false;
}

// Cycle Detection Function 
bool isCyclic(struct Graph* graph) {
    bool visited[graph->V];
    for (int i = 0; i < graph->V; i++)
        visited[i] = false;

    for (int i = 0; i < graph->V; i++) {
        if (!visited[i]) {
            if (DFSUtil(graph, i, visited, -1))
                return true;
        }
    }
    return false;
}

int main() {
    /*
        Example Graph with a cycle:
            0 -- 1
            |  /
            2
    */

    int V = 3;
    struct Graph* graph = createGraph(V);

    addEdge(graph, 0, 1);
    addEdge(graph, 1, 2);
    addEdge(graph, 2, 0);

    if (isCyclic(graph))
        printf("Graph contains a cycle\n");
    else
        printf("Graph does not contain a cycle\n");

    return 0;
}


```

## Example Output:

```c

Graph contains a cycle

```

## If you remove the edge (2, 0), the output will be:

```c

Graph does not contain a cycle

```
