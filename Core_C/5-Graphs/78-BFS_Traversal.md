# Write a program to perform a Breadth-First Search (BFS) traversal on a graph starting from a given source node.

```c

#include <stdio.h>
#include <stdlib.h>

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

// Queue for BFS
struct Queue {
    int items[100];
    int front, rear;
};

// Queue Functions 
void initQueue(struct Queue* q) {
    q->front = -1;
    q->rear = -1;
}

int isEmpty(struct Queue* q) {
    return q->front == -1;
}

void enqueue(struct Queue* q, int value) {
    if (q->rear == 99) {
        printf("Queue Overflow!\n");
        return;
    }
    if (q->front == -1) q->front = 0;
    q->items[++q->rear] = value;
}

int dequeue(struct Queue* q) {
    if (isEmpty(q)) {
        printf("Queue Underflow!\n");
        return -1;
    }
    int item = q->items[q->front];
    if (q->front == q->rear) {
        q->front = q->rear = -1;
    } else {
        q->front++;
    }
    return item;
}

// Create new adjacency list node 
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

// Add Edge (Undirected Graph) 
void addEdge(struct Graph* graph, int src, int dest) {
    struct Node* newNode = createNode(dest);
    newNode->next = graph->array[src].head;
    graph->array[src].head = newNode;

    newNode = createNode(src);
    newNode->next = graph->array[dest].head;
    graph->array[dest].head = newNode;
}

// BFS Traversal 
void BFS(struct Graph* graph, int startVertex) {
    int* visited = (int*)malloc(graph->V * sizeof(int));
    for (int i = 0; i < graph->V; i++)
        visited[i] = 0;

    struct Queue q;
    initQueue(&q);

    visited[startVertex] = 1;
    enqueue(&q, startVertex);

    printf("BFS Traversal starting from vertex %d: ", startVertex);

    while (!isEmpty(&q)) {
        int currentVertex = dequeue(&q);
        printf("%d ", currentVertex);

        struct Node* temp = graph->array[currentVertex].head;
        while (temp) {
            int adjVertex = temp->dest;
            if (!visited[adjVertex]) {
                visited[adjVertex] = 1;
                enqueue(&q, adjVertex);
            }
            temp = temp->next;
        }
    }
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
    addEdge(graph, 2, 3);

    BFS(graph, 0);

    return 0;
}


```

## Example Output:

```c

BFS Traversal starting from vertex 0: 0 2 1 3

```
