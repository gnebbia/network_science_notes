# Betweenness Centrality

Betweenness centrality is another centrality meaasure where
the basic assumption is that important nodes connect other
nodes.

Recall that the distance between two nodes is the length of
the shortest path between them.

So here we evaluate the importance of a node by looking at
how frequently this node appears in shortest paths between
any node pair.
The betweenness centrality for a node 'V' is computed as:
`Cbtw(V) = sum(sigma_s_t(V) / sigma_s_t)`
where:
- `sigma_s_t(V)` is the number of shortest paths between node S and node T who pass through V in their path
- `sigma_s_t` is the number of shortest paths between node S and node T

This must be done for all nodes S and T.
Note that in this measure we can either include or exclude node V
as node S and T in the computation of Cbtw(V).
Of course if we include the node V as node S and T we get a higher measure
of betweenness centrality.

## Betweenness Centrality in Disconnected Nodes

What happens to the computation when a node is disconnected or
cannot be reached by any other node?
Note that this would make its sigma equal to zero making the
previous definition undefined.

So in this case, we can fix the formula by considering only nodes
S and T such that there is at least one path between them.

## Normalizing the Betweenness Centrality

Note that if we strictly follow the above definition, then what happens
is that betweenness centrality values will be larger in graphs with many nodes
but it will be lower in smaller graphs with less nodes.
To control this, when we compute betweenness centrality it is a good idea
to normalize our results. To normalize our results we do this:
- Take the betweenness centrality measure of nodes in the graph 
- Didivde this centrality measure by the number of pairs of nodes in the graph (excluding V),
  this number is equal to:
  - (1/2)(|N|-1)(|N|-2) in **undirected** graph;
  - (|N|-1)(|N|-2) in **directed** graph;


In networkx we can compute betweenness centrality by doing:
```python
# This is the recommended way to compute Betweenness centrality, hence
# by excluding the node itself from the computation and normalizing
# the results
btwnCent = nx.betweenness_centrality(G, normalized=True, endpoints=False)
```

Note that normalizing is particularly important whenever we want to compare
betweenness centrality values among different networks which have different
sizes.

## Computational Cost

A problem associated with betweenness centrality is that it is
computationally expensive.
Depending on the algorithm, this computation can take up to O(|N|^3)
in time.

Consider that for a network of about 2200 nodes we have roughly 4.8 milion
of pairs of nodes.

So what is done generally is that rather than computing betweenness centrality
based on all pairs of nodes S,T we can approximate it based on a sample
of nodes.

Different choices are possible for the sample/subset of nodes:
- random sample (when we have no preference and just want a sample);
- specific subset (when we are interested in betweenness centrality only within a specific set of nodes);

### Random Sample Betweenness Centrality Approximation

So for large networks we can apply this principle in networkx, and
get a random sample of the entire network by doing:
```python
# In this case we consider a sample of 10 nodes
btwnCent = nx.betweenness_centrality(G, normalized=True, endpoints=False, k=10)
```

### Specific Subset Betweenness Centrality Approximation

We can choose a specific subset of nodes if we are interested in understanding
what is the betweenness centrality among a set of source nodes and another set
of target nodes.
In networkx we can do it like this:
```python
btwnCent = nx.betweenness_centrality_subset(G,
                            ['A','B','C','D','K','Y'],
                            ['P','Z','Q','R'], normalized=True)
```
Note that in this last case, in the list of nodes with highest betweenness
centrality we can of course get also nodes which are not in the source
subset of in the target subset.  Becase, recall, that the aim is to find
in the entire network who are the central nodes, in this case the most
important nodes in terms of connection and shortest paths which connect
the specified sources to the specified targets.


## Betweenness Centrality of Edges

Note that everything explained above can be specularly applied to edges.
So we can understand what are the most important edges in terms of
connectivity in a network.
Basically the sigmas won't represent in this case the number of shortest
paths between node S and node T. On the contrary, sigmas will represent
the number of shortest paths between nodes S and T passing through edge E.

In networkx we can compute the edge centrality by doing:
```python
btwnCent = nx.edge_betweenness_centrality(G, normalized=True)
```

We can of course also in this case use the subset technique for edges:
```python
btwnCent = nx.edge_betweenness_centrality_subset(G,
                            ['A','B','C','D','K','Y'],
                            ['P','Z','Q','R'], normalized=True)
```
