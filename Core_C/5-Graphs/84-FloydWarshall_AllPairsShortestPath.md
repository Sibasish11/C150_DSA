# Write a program to implement the Floyd-Warshall algorithm to find all-pairs shortest paths in a weighted graph.

```c

#include <stdio.h>
#include <limits.h>

#define V 4
#define INF 99999 // Representation of infinity

// Floyd-Warshall algorithm
void floydWarshall(int graph[V][V]) {
    int dist[V][V];

    // Step 1: Initialize distance matrix as input graph
    for (int i = 0; i < V; i++)
        for (int j = 0; j < V; j++)
            dist[i][j] = graph[i][j];

    // Step 2: Update distances using intermediate vertices
    for (int k = 0; k < V; k++) {
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {
                if (dist[i][k] + dist[k][j] < dist[i][j])
                    dist[i][j] = dist[i][k] + dist[k][j];
            }
        }
    }

    // Step 3: Print shortest distance matrix
    printf("All-Pairs Shortest Path Matrix:\n");
    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            if (dist[i][j] == INF)
                printf("%7s", "INF");
            else
                printf("%7d", dist[i][j]);
        }
        printf("\n");
    }
}

int main() {
    /*
        Example Graph:
        (Adjacency Matrix Representation)
        INF means no direct edge
            0    5    INF  10
            INF  0    3    INF
            INF  INF  0    1
            INF  INF  INF  0
    */

    int graph[V][V] = {
        {0,   5,  INF, 10},
        {INF, 0,   3,  INF},
        {INF, INF, 0,   1},
        {INF, INF, INF, 0}
    };

    floydWarshall(graph);

    return 0;
}


```

## Example Output:

```csharp

All-Pairs Shortest Path Matrix:
      0      5      8      9
    INF      0      3      4
    INF    INF      0      1
    INF    INF    INF      0

```
