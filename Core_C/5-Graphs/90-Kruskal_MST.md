# Implement a program to find the Minimum Spanning Tree (MST) of a graph using Kruskal's algorithm (requires a Disjoint Set Union data structure).

```c

#include <stdio.h>
#include <stdlib.h>

struct Edge {
    int u, v, w;
};

struct Subset {
    int parent;
    int rank;
};

// Find with path compression
int find(struct Subset subsets[], int i) {
    if (subsets[i].parent != i)
        subsets[i].parent = find(subsets, subsets[i].parent);
    return subsets[i].parent;
}

// Union by rank
void unionSets(struct Subset subsets[], int x, int y) {
    int rootX = find(subsets, x);
    int rootY = find(subsets, y);

    if (subsets[rootX].rank < subsets[rootY].rank)
        subsets[rootX].parent = rootY;
    else if (subsets[rootX].rank > subsets[rootY].rank)
        subsets[rootY].parent = rootX;
    else {
        subsets[rootY].parent = rootX;
        subsets[rootX].rank++;
    }
}

// Compare function for qsort
int compareEdges(const void* a, const void* b) {
    struct Edge* e1 = (struct Edge*)a;
    struct Edge* e2 = (struct Edge*)b;
    return e1->w - e2->w;
}

// Kruskal's Algorithm
void kruskalMST(struct Edge edges[], int V, int E) {
    qsort(edges, E, sizeof(struct Edge), compareEdges);

    struct Subset* subsets = (struct Subset*)malloc(V * sizeof(struct Subset));
    for (int v = 0; v < V; v++) {
        subsets[v].parent = v;
        subsets[v].rank = 0;
    }

    int mstWeight = 0;
    printf("Edges in MST:\n");

    int e = 0; // count of edges in MST
    for (int i = 0; i < E && e < V - 1; i++) {
        int u = edges[i].u;
        int v = edges[i].v;

        int rootU = find(subsets, u);
        int rootV = find(subsets, v);

        if (rootU != rootV) {
            printf("%d - %d   %d\n", u, v, edges[i].w);
            mstWeight += edges[i].w;
            unionSets(subsets, rootU, rootV);
            e++;
        }
    }

    printf("Total weight of MST: %d\n", mstWeight);

    free(subsets);
}

int main() {
    int V, E;
    printf("Enter number of vertices: ");
    scanf("%d", &V);
    printf("Enter number of edges: ");
    scanf("%d", &E);

    struct Edge* edges = (struct Edge*)malloc(E * sizeof(struct Edge));

    printf("Enter edges (u v w):\n");
    for (int i = 0; i < E; i++) {
        scanf("%d %d %d", &edges[i].u, &edges[i].v, &edges[i].w);
    }

    kruskalMST(edges, V, E);

    free(edges);
    return 0;
}


```

## Example Run:

### Input:

```c

Enter number of vertices: 4
Enter number of edges: 5
0 1 10
0 2 6
0 3 5
1 3 15
2 3 4

```

### Output:

```c
Edges in MST:
2 - 3   4
0 - 3   5
0 - 1   10
Total weight of MST: 19
```
