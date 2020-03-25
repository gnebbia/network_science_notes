# Distance

Introducing distance measures is fundamental in a network and allows us
to reply to many questions such as: "How far is node A from node K ?",
"Are nodes far away or close to each other in this network?", "Which
nodes are closest or fathest to other nodes?".

We first have to introduce the concept of **path**, which is
a sequence of nodes connected by an edge.
We can then define as **path length** the number of steps it
contains from the beginning to end.

## Distance between two Nodes

To define the **distance between two nodes** we can take the length
of the shortest path between these two nodes.

In networkx we can compute the distance by doing:
```python
# Get the entire path between two nodes on a graph G
nx.shortest_path(G,'A','K')

# Get only the number of hops between two nodes (distance) on a graph G
nx.shortest_path_length(G,'A','K')
```

## Distance between a Node and all other nodes

Sometimes we want to understand how far is a specific node 'A' with
respect to all other nodes in a network.
This operation is easy to do manually in small networks but tedious
in large (more real world) networks.

To do this there are different strategies, and one is called
breadth-first search.  **Breadth-first search** (BFS) is a systematic and
efficient procedure for computing distances from a node to all other
nodes in a large network by "discovering" nodes in layers.
The BFS algorithm outputs a tree where each layer corresponds to a distance
and all nodes contained in a layer are nodes at that distance from the root node.
So if the root node is A, then we are considering all the distances from node A.
At layer 1, we will have all nodes which are distant 1 hop from node A, at layer 2
we have all nodes which are distant 2 hops from node A and so on.
In networkx we can discover the entire distance tree with respect to a node by
using BFS like this:
```python
T = nx.bfs_tree(G,'A')
```

If we are not interested in the tree, but just want a dictionary
of the distances between a node and all other nodes we can do:
```python
nx.shortest_path_length(G,'A')
```


## Distance of the entire Network

We can characterize the distance between all pairs of nodes in a graph.
There are different ways to describe the overall distance in a network:
- Average Distance;
- Diameter;
- Eccentricity;
- Radius;

### Average Distance

One way to do this is through the **average distance**, which is the
average of the distance between nevery pair of nodes.
In networkx we can compute this by doing:
```python
nx.average_shortest_path_length(G)
```

### Diameter

We can also measure the **diameter** which is the maximum distance between
any pair of nodes.
```python
nx.diameter(G)
```

### Eccentricity

We can additionally measure the **eccentricity** which is the maximm length
path for each node in a graph, and this gives us a set of numbers (not a single
measure) representing the maximum path lengths for each node in the graph.
In networkx we can get the dictionary related to eccentricity like this:
```python
nx.eccentricity(G)
# Out: {'A':5,'B':4,'C':8,'D':3 ... }
```

### Radius

The **radius** of a network is derived from the eccentricity and corresponds to the
minimum eccentricity value in a network.

So given the following eccentricity hashmap: `{'A':5,'B':4,'C':8,'D':3}`,
the radius is equal to 3, which corresponds to the eccentricity of 'D'.

In networkx we can get the radius of a network by doing:
```python
nx.radius(G)
```

## Other definitions related to Distance

### Periphery

The **periphery** of a graph is the set of nodes that have
eccentricity equal to the diameter.
In networkx we can get the periphery set of nodes by doing:
```python
nx.periphery(G)
```

### Center

The **center** of a graph is the set of nodes that have eccentricity equal
to the radius.
In networkx we can get the center set of nodes by doing:
```python
nx.center(G)
```

