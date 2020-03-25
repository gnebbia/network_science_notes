# Connectivity

## Connectivity in Undirected Graphs

An undirected graph is **connected** if, for
every pair of nodes, there is a path between them.

We can check if a graph is connected in networkx by doing:
```python
nx.is_connected(G)
# gives True/False
```

### Connected Components in Undirected Graphs

We can also define **connected components** as the subset
of nodes such as:
1. every node in the subset has a path to every other node;
2. no other node has a path to any node in the subset;

Connected components correspond to **communities** in a graph.

We can find the number of connected components in networkx by doing:
```python
nx.number_connected_components(G)
```
We can aso get the sets related to the connected components by doing:
```python
sorted(nx.connected_components(G))
```

We can also get the community (i.e., connected component) related to a
specific node by doing:
```python
# Get the community (aka connected component) of M
nx.node_connected_component(G,'M')
```

## Connectivity in Directed Graphs

When it comes to directed graphs we can distinguish between
two kinds of connectivity:
- Strongly Connected Graphs;
- Weakly Connected Graphs;

A directed graph is **strongly connected** if, for
every pair of nodes *u* and *v*, there is a directed
path from u to v and another directed path from v to u.

We can check if a directed graph is strongly connected in networkx
by doing:
```python
nx.is_stronly_connected(G)
# gives True/False
```

A directed graph is **weakly connected** if, replacing all
directed edges with undirected edges produces a connected
undirected graph.

We can check if a directed graph is weakly connected in networkx by doing:
```python
nx.is_weakly_connected(G)
# gives True/False
```

### Connected Components in Directed Graphs

In directed graphs we have two kinds of connected components:
- Strongly Connected Components;
- Weakly Connected Components;

#### Strongly Connected Components

We can define **strongly connected components** as the subset
of nodes such as:
1. every node in the subset has a *directed* path to every other node;
2. no other node has a *directed* path to and from every node in the subset;

Connected components correspond to **communities** in a graph.
Basically a strongly component correspond to a community where each node
can reach any other node (it's not really like these, there are more details
to add but it is a simplified idea).

We can find the number of strongly connected components in networkx by doing:
```python
nx.number_strongly_connected_components(G)
```
We can aso get the sets related to the strongly connected components by doing:
```python
sorted(nx.strongly_connected_components(G))
```

#### Weakly Connected Components

We can define **weakly connected components** as the subset
of nodes such as if we convert the directed grapph to an undirected
one we have the same conditions applying for undirected connected components.

Connected components correspond to **communities** in a graph.
Basically a weakly connected component corresponds to a connected
component in an undirected graph.

We can find the number of weakly connected components in networkx by doing:
```python
nx.number_weakly_connected_components(G)
```
We can aso get the sets related to the weakly connected components by doing:
```python
sorted(nx.weakly_connected_components(G))
```

### Examples of Strongly/Weakly Connected Components

A network is not strongly connected when some pairs of nodes do not have
a path connecting them. For example, if there is no path from node C to
node D (there could also be a path from D to C but if there is no path
from C to D the network is not strongly connected). On the contrary,
a network is weakly connected when replacing all directed edges with
undirected edges produces a connected undirected graph.
