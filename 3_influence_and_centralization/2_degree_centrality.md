# Degree Centrality

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
