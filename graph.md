# Graph Representation

## 1. Adjacency Matrix

### Despription
- A 2D matrix 'graph[u][v]' where a non-zero value indicates an edge from 'u' to 'v'.
- Best for dense graphs.

### code
```cpp
const int MAXN = 100;
int graph[MAXN][MAXN];

void addEdge(int u, int v, int w = 1) {
    graph[u][v] = w;
}

bool hasEdge(int u, int v) {
    return graph[u][v] != 0;
}
```

## 2. Adjacency List

### Despription
- Each node holds a list of adjacent nodes.
- Suitable for sparse graphs.

### code
```cpp
#include <vector>
using namespace std;

const int MAXN = 100;
vector<int> adj[MAXN];

void addEdge(int u, int v) {
    adj[u].push_back(v);
}
```

## 3. Edge Set

### Despription
- Store each edge as a struct or tuple.

### code
```cpp
#include <vector>
using namespace std;

struct Edge {
    int u, v, w;
};

vector<Edge> edges;

void addEdge(int u, int v, int w = 1) {
    edges.push_back({u, v, w});
}
```

## 4. Linked Forward Star

### Despription
- Array-based optimized adjacency list.
- Extremely efficient for static sparse graphs.

### code
```cpp
#include <iostream>
#include <cstring>
using namespace std;

const int MAXN = 100005;
const int MAXM = 200005;

int head[MAXN], to[MAXM], nextEdge[MAXM], weight[MAXM];
int edgeCount = 0;

void initGraph(int n) {
    memset(head, -1, sizeof(int) * (n + 1));
    edgeCount = 0;
}

void addEdge(int u, int v, int w = 1) {
    to[edgeCount] = v;
    weight[edgeCount] = w;
    nextEdge[edgeCount] = head[u];
    head[u] = edgeCount++;
}

void traverse(int u) {
    for (int i = head[u]; i != -1; i = nextEdge[i]) {
        int v = to[i];
        int w = weight[i];
        // process edge u → v with weight w
    }
}
```

## Graph Representation Comparison Table

| Representation        | Lookup Time | Insert Time | Space Complexity | Best Use Case                        |
|------------------------|--------------|--------------|-------------------|--------------------------------------|
| **Adjacency Matrix**   | O(1)         | O(1)         | O(N²)             | Dense graphs, fast existence checks  |
| **Adjacency List**     | O(k)         | O(1)         | O(N + M)          | Most common, good for sparse graphs  |
| **Edge List / Set**    | O(M)         | O(1)         | O(M)              | Sorting edges, Kruskal's algorithm   |
| **Linked Forward Star**| O(k)         | O(1)         | O(N + M)          | Fastest static graph access (contests) |
