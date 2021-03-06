## Degree Centrality

The assumption behind degree centrality is that important nodes
have many connections. Hence here we measure the importance
by looking at the degree of each node, that is, the number of
connections it has.

This is the most basic measure of network centrality.

Degree can be of two types depending on the type of network we analyze:
- for Undirected networks we just talk about **degree**;
- for Directed networks we can talk about **in-degree** or **out-degree**;

We can define degree centrality as:
`C_deg(v) = Dv / (|N| - 1)`
where:
- Dv is the degree of the node V
- N is the set of nodes

This measure goes from 0 to 1.
Hence a node has a degree centrality of 1 if it is connected to all nodes in
a network and 0 if it is not connected to any nodes in the network.

In networkx we can find node centrality in this way:
```python
nx.degree_centrality(G)
# This returns a dictionary of degree centrality measures for each node in the network
```

In directed networks we can define in-degree centrality like this:
`C_indeg(v) = Dv_in / (|N| - 1)`
where:
- Dv is the degree of the node V for incoming edges
- N is the set of nodes

and and out-degree centralities like this:
`C_outdeg(v) = Dv_out / (|N| - 1)`
where:
- Dv_out is the degree of the node V for outgoing edges
- N is the set of nodes

In networkx we can compute them like this:
```python
# In-Degree Centrality
indegCent = nx.in_degree_centrality(G)

# Out-Degree Centrality
outdegCent = nx.out_degree_centrality(G)
```


## Closeness Centrality

In closeness centrality the basic assumption is that important nodes
are the ones closer to other nodes.

We can compute closeness centrality with:
`Cclose(v) = (|N| - 1) / (sum(d(v,u))`
where:
- N is the number of nodes;
- d(v,u) is the length of the shortest path from v to u;

In networkx we can find the closeness centrality by doing:
```python
closeCent = nx.closeness_centrality(G)
# This returns a dictionary with measures for each node

# We can query the closeness centrality for a specific node by doing:
closeCent['A']

# which without the closeness_centrality function could be manually computed (and is equivalent to) as:
# (len(G.nodes()) - 1) / sum(nx.shortest_path_length(G,'A').values()
```

### Closeness Centrality in Disconnected Networks

How can we measure the closeness centrality of a node when
it cannot reach all other nodes?
We have different options in this case:
**Option I**: we consider only nodes that a node L can reach:
`Cclose(L) = |R(L)| / (sum(d(L,u)))`
where:
- R(L) is the set of nodes L can reach
- sum(d(L,u)) is the sum of all the shortest paths from L to the nodes that L can reach

Anyway we have problem with this option, because let's say for example that
from node L we can only reach node M which is 1 hop away. At this point,
if we apply the formula we get a closeness centrality of 1(maximum), although this node
is not very central/important in the network.
Another example can be a simple graph like this:
`A -> B -> C -> D`
in this case under option I node C has closeness centrality of 1, the
highest of all nodes, because it can only reach D and it reaches in
one step.

In networkx we can still use option I to compute closeness centrality by doing:
```python
closeCent = nx.closeness_centrality(G, normalized=False)
# This returns a dictionary with all closeness centrality measures

# Access the closeness centrality meaasure of L
closeCent['L']
```




**Option II (Better)**: we consider only nodes that a node L can reach, but
normalize with respect the total number of nodes in the network, hence:
`Cclose(L) = (|R(L)| / |N - 1|) * ( |R(L)| / (sum(d(L,u))) )`
where:
- R(L) is the set of nodes L can reach
- N is the total number of nodes in the network
- sum(d(L,u)) is the sum of all the shortest paths from L to the nodes that L can reach


In networkx the option II is the default option when we compute closeness centrality,
and this can be done with:
```python
closeCent = nx.closeness_centrality(G, normalized=True)
# This returns a dictionary with all closeness centrality measures

# Access the closeness centrality meaasure of L
closeCent['L']
```
An example can be a simple graph like this:
`A -> B -> C -> D`
Under option 2, node A has closeness centrality of 1/2, the highest of
all nodes. A can reach all other nodes in the network: B in 1 step,
C in 2 steps, and D in 3 steps. Hence, A's closeness centrality is 1/2.
