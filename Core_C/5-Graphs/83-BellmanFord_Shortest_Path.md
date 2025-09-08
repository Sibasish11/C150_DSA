# Develop a program to find the shortest path from a source to all other vertices using Bellman-Ford algorithm (handle negative edge weights and detect negative cycles).

```c

#include <stdio.h>
#include <stdlib.h>
#include <limits.h>

// Edge Structure 
struct Edge {
    int src, dest, weight;
};

// Graph Structure 
struct Graph {
    int V, E;
    struct Edge* edge;
};

// Create Graph
struct Graph* createGraph(int V, int E) {
    struct Graph* graph = (struct Graph*)malloc(sizeof(struct Graph));
    graph->V = V;
    graph->E = E;
    graph->edge = (struct Edge*)malloc(E * sizeof(struct Edge));
    return graph;
}

// Bellman-Ford Algorithm
void BellmanFord(struct Graph* graph, int src) {
    int V = graph->V;
    int E = graph->E;
    int dist[V];

    // Step 1: Initialize distances
    for (int i = 0; i < V; i++)
        dist[i] = INT_MAX;
    dist[src] = 0;

    // Step 2: Relax edges (V-1 times)
    for (int i = 1; i <= V - 1; i++) {
        for (int j = 0; j < E; j++) {
            int u = graph->edge[j].src;
            int v = graph->edge[j].dest;
            int weight = graph->edge[j].weight;

            if (dist[u] != INT_MAX && dist[u] + weight < dist[v])
                dist[v] = dist[u] + weight;
        }
    }

    // Step 3: Check for negative weight cycles
    for (int j = 0; j < E; j++) {
        int u = graph->edge[j].src;
        int v = graph->edge[j].dest;
        int weight = graph->edge[j].weight;

        if (dist[u] != INT_MAX && dist[u] + weight < dist[v]) {
            printf("Graph contains a negative weight cycle!\n");
            return;
        }
    }

    // Print results
    printf("Vertex \t Distance from Source %d\n", src);
    for (int i = 0; i < V; i++)
        printf("%d \t %d\n", i, dist[i]);
}

int main() {
    /*
        Example Graph:
        Vertices = 5, Edges = 8
        Edge List:
        0 -> 1 (weight -1)
        0 -> 2 (weight 4)
        1 -> 2 (weight 3)
        1 -> 3 (weight 2)
        1 -> 4 (weight 2)
        3 -> 2 (weight 5)
        3 -> 1 (weight 1)
        4 -> 3 (weight -3)
    */

    int V = 5; // number of vertices
    int E = 8; // number of edges
    struct Graph* graph = createGraph(V, E);

    graph->edge[0].src = 0; graph->edge[0].dest = 1; graph->edge[0].weight = -1;
    graph->edge[1].src = 0; graph->edge[1].dest = 2; graph->edge[1].weight = 4;
    graph->edge[2].src = 1; graph->edge[2].dest = 2; graph->edge[2].weight = 3;
    graph->edge[3].src = 1; graph->edge[3].dest = 3; graph->edge[3].weight = 2;
    graph->edge[4].src = 1; graph->edge[4].dest = 4; graph->edge[4].weight = 2;
    graph->edge[5].src = 3; graph->edge[5].dest = 2; graph->edge[5].weight = 5;
    graph->edge[6].src = 3; graph->edge[6].dest = 1; graph->edge[6].weight = 1;
    graph->edge[7].src = 4; graph->edge[7].dest = 3; graph->edge[7].weight = -3;

    BellmanFord(graph, 0);

    return 0;
}


```

## Example Output:

```csharp

Vertex   Distance from Source 0
0        0
1       -1
2        2
3       -2
4        1

```
