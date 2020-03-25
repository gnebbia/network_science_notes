# Robustness

In network science we define as **network robustness** the ability of
a network to maintain its general structural properties when it faces
failures or attacks.

The structural properties we refer to is **connectivity**.
The attacks we refer to here are removal of nodes or edges.

Examples here can be, "What is the impact of some airport closure?",
"What is the impact of some internet router failures?", "What is
the impact of some power line failures?".

We can define as **node connectivity** the minimum number of nodes needed
to disconnect a graph or a specific pair of nodes.

We can define as **edge connectivity** the minimum number of edge needed
to disconnect a graph or a specific pair of nodes.

Graphs with large node and edge connectivity are more roobust to the
loss of nodes and edges.


## Disconnecting a Graph

We can understand what is the smallest number of nodes that can be
removed from this graph in order to disconnect it; so to transform
a connected graph to an unconnected graph.

In networkx we can understand how may nodes we have to delete
to make a connected graph disconnected with:
```python
nx.node_connectivity(G_undirected)
# The output is a number representing the minimum number of nodes
# which we need to cut to transform the connected network in a disconnected network
```
We can also get which node we should delete to transform the network in a disconnected
network by doing:
```python
nx.minimum_node_cut(G_undirected)
## Note that the choice of the node is not unique, but neetworkx just provides one choice
```

We can also understand how to disconnect a network in terms of edges, so
in networkx we can do:
```python
# Get the number of edge to remove to disconnect the network
nx.edge_connectivity(G_undirected)
# Get the edge to remove to disconnect the network
nx.minimum_edge_cut(G_undirected)
## Note that the choice of the edge is not unique, but neetworkx just provides one choice
```

In these terms, a robust network is a network where we should remove a
large number of edges or nodes in order to disconnect it.

## Simple Paths

Imagine that a node G wants to send a message to a node L in a directed graph.
We can get all possible paths from G to L in networkx by doing:
```python
sorted(nx.all_simple_paths(G,'G','L'))
```

With directed graphs we have the same functions as with undirected graphs to
understand how to cut network connectivity, but in addition to passing
a directed graph we have to pass the two nodes for which we want to cut
the relationship, so we can do:
```python
# Get the number of nodes to remove to disconnect the path from G to L
nx.node_connectivity(G,'G','L')
# Get the nodes to remove to disconnect the path from G to L
nx.minimum_node_cut(G,'G','L')
```

We can also do the same thing with edges, so for example we can understand
how many edges an attacker should remove to disconnect two nodes.
In networkx we can do it like this:
```python
# Get the number of nodes to remove to disconnect the path from G to L
nx.edge_connectivity(G,'G','L')
# Get the nodes to remove to disconnect the path from G to L
nx.minimum_edge_cut(G,'G','L')
```

