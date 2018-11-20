# Graph

## What is a Graph?

A graph is a non-linear data structure consisting of vertices connected by edges.

Graphs can be:

- Weighted or Unweighted
  - A value is assigned (or not assigned) to the distances between vertices
- Directed or Undirected
  - Directions are assigned (or not assigned) between vertices

Graphs can be used for building:

- Maps
- Social Networks
- Recommendation systems

## Storing Vertices and Edges

The graph and its vertices and edges can be represented in the following ways:

- **Adjacency Matrix**
  - A matrix maps a vertex's relationship to _every other vertex_. This can be accomplished by indicating 0 for no edge (connection) between vertices or 1 to indicate an edge exists between vertices.
  * Since all relationships are mapped, whether there is a connection or not, an adjacency matrix can be faster than an adjacency list for looking up a specific edge, although at a cost of taking up more memory space and being slower in iterating over all edges.
- **Adjacency List**
  - A list maps only each vertex's adjacent vertices (ie. neighbouring nodes).
  * Since only adjacent vertices are mapped for each vertex, iterating over all edges is faster than in an adjacency matrix but slower for looking up a specific edge.

**Note**

## Creating the Graph Class

```javascript
class Graph {
  constructor() {
    this.adjacencyList = {};
  }
}
```

The adjacency list holds all of the vertices and each vertex holds connections to other vertices (adjacent vertices).

## Adding Methods

### Adding a vertex

Adds a vertex to the graph.

#### Code

```javascript
  addVertex(vertex) {
    if (!this.adjacencyList[vertex]) this.adjacencyList[vertex] = [];
  }
```

### Adding an Edge

Adds an edge(or a connection) to the specified vertex.
