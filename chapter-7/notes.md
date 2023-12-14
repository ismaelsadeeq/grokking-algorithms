There is a limitation to the BFS algorithm though, the shortest path to X does not necessarily mean indicating that that's the fastest path to X. There are some graphs where the edges are weighted which might indicate the distance between nodes.

In such cases, the algorithm to employ for calculating the shortest and fastest path to X is <b>the Dijikstra Algorithm.</b>

Dijikstra is an interesting algorithm that operates on a weighted directed acyclic graph.

The steps of Dijikstra Algorithm

1. Find the “cheapest” node that has not been explored. E.g. the node you can get to in the least amount of time.
2. Update the costs of the neighbours of this node.
3. Repeat until you’ve done this for every node in the graph.
4. Calculate the final path. which is the amount of hops that take you to the destination node cheaper.


Implementation of Dijikstra Algorithm

```python
class Graph:
    def __init__(self):
        self.g = {}

    def addNode(self, node):
        if node in self.g:
            return
        self.g[node] = {}

    def addEdge(self, node, edge, weight):
        self.addNode(node)
        self.g[node][edge] = weight

    def find_lowest_cost_node(self, costs, processed):
        lowest_cost = float("inf")
        lowest_cost_node = None
        for node in costs:
            cost = costs[node]
            if cost < lowest_cost and node not in processed:
                lowest_cost = cost
                lowest_cost_node = node
        return lowest_cost_node

    def dijikstra_search(self, start, node):
        costs = {}
        parents = {}
        for key in self.g[start].keys():
            costs[key] = self.g[start][key]
            parents[key] = start

        if node not in costs:
            costs[node] = float("inf")
    
        processed = []
        candidate_node =  self.find_lowest_cost_node(costs, processed)
        # while we have nodes to process:
        while candidate_node is not None:
            # take node close to start
            cost = costs[candidate_node]
            neigbors = self.g[candidate_node]
            # update neighbors costs
            for n in neigbors.keys():
                new_cost = cost + neigbors[n]
                if n not in costs:
                     costs[n] = new_cost
                     parents[n] = candidate_node
                elif new_cost < costs[n]:
                    costs[n] = new_cost
                    # if any of the neigbors cost were updated, update parents also
                    parents[n] = candidate_node
            # mark the node as processed 
            processed.append(candidate_node)
            candidate_node = self.find_lowest_cost_node(costs, processed)

        return parents, costs[node]

    def getGraph(self):
        return self.g
        
g = Graph()
g.addEdge('start', 'A', 6)
g.addEdge('start', 'B', 2)
g.addEdge('A', 'f', 1)
g.addEdge('B', 'A', 3)
g.addEdge('B', 'f', 5)
g.addNode('f')

print(g.dijikstra_search('start', 'f'))

g2 = Graph()
g2.addEdge('start', 'A', 5)
g2.addEdge('start', 'B', 2)
g2.addEdge('B', 'A', 8)
g2.addEdge('B', 'D', 7)
g2.addEdge('A', 'C', 4)
g2.addEdge('A', 'D', 2)
g2.addEdge('D', 'f', 1)
g2.addEdge('C', 'D', 6)
g2.addEdge('C', 'f', 3)
g2.addNode('f')
print(g2.dijikstra_search('start', 'f'))

g3 = Graph()
g3.addEdge('start', 'A', 10)
g3.addEdge('A', 'B', 20)
g3.addEdge('B', 'C', 1)
g3.addEdge('C', 'A', 1)
g3.addEdge('B', 'f', 30)
g3.addNode('f')
print(g3.dijikstra_search('start', 'f'))


```
Limitation of Dijikstra algorithm is that it does not work on a graph that has negative edges.
see https://www.geeksforgeeks.org/why-does-dijkstras-algorithm-fail-on-negative-weights/

You can use Bellman-Ford Algorithm for that type of problems
