Graph Data Structure

A graph represents a series of nodes connected by edges, where nodes may or may not be weighted, similar to the edges.

We can model relationships between people using graphs.

Breadth-First Search (BFS)

BFS is a process applied to a graph to find nodes with a specific value, starting from the initial node. It involves traversing through connected nodes, exploring edges and searching for nodes connected to those. This method allows us to identify the first occurrence of the value and determine the shortest path to that node.

Therefore, BFS answers two critical questions regarding a given graph:

1. Is there a path to a node with the desired value?
2. What is the shortest path to reach that particular node?

Queues

A queue is a data structure that adheres to the first-in, first-out (FIFO) principle, similar to a physical queue. In a queue, the first element added is the first to be removed, and the last element added is the last to be removed. This concept is analogous to people standing in a queue, where the first person to join will be the first to leave.


Implementation of graph

One way we can implement graph data structure is through a hash table we can use the key to represent the nodes and values the edges each node is connected to.

```python
graph = {}
graph['A'] = ['B']
graph['B'] = ['C', 'E']
graph['C'] = ['D']
graph['E'] = ['F']
graph['D'] = ['F']
```


The we can run a breath first search on this graph hash table to check whether an element exist.
Whether their is a path to from node A to an the element in the graph and the shortest path to that element also.

Breath First Search Algorithm

```python
class Graph:
    g = {}

    def addNode(self, node):
        if node in self.g:
            return
        self.g[node] = []

    def addEdge(self, node, e):    
        if node not in self.g or e not in self.g:
            return
        if e in self.g[node]:
            return
        self.g[node].append(e)

    def bfs(self, start, element):
        if start not in self.g:
            print("Start node not in graph")
            return False

        visited = []
        queue = [start]

        while queue:
            current_node = queue.pop(0)

            if current_node == element:
                visited.append(current_node)
                print(visited)
                return True

            if current_node not in visited:
                visited.append(current_node)
                neighbors = self.g.get(current_node, [])
                queue.extend(neighbors)

        print(list(visited))
        return False

graph = Graph()

graph.addNode('A')
graph.addNode('B')
graph.addNode('C')
graph.addNode('D')
graph.addNode('E')
graph.addNode('F')
graph.addEdge('A', 'B')
graph.addEdge('B', 'C')
graph.addEdge('B', 'E')
graph.addEdge('C', 'D')
graph.addEdge('D', 'F')
graph.addEdge('E', 'F')
print(graph.bfs('A', 'E'))
```
The above implementation of graph is known is adjacency list, there is also another implementation of graph using adjacency matrix.


Whenever you come across a problem where you need to find the shortest path to X, you can model the problem in a graph data structure and use breadth-first search to solve it.

