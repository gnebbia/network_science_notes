# Bipartite Graphs

Bipartite graphs are a particular kind of graphs
where there is a specific structure.
The structure is generally where a specific kind
of nodes has a specific relation with another set of nodes.

All the edges go from one set of nodes to another set of nodes.
Think about the relationship between "fans" and "soccer teams".
We only have fans which support a soccer team, but we don't have
fans which are fans of other fans or soccer teams who are fans of
fans.

To be more precise, a graph is a **bipartite graph** if its
nodes can be split into two sets L and R and every edge connects
a node in L with a node in R.

Let's see how to work with bipartite graphs in networkx.
```python
from networkx.algorithms import bipartite
B = nx.Graph()
B.add_nodes_from(['A','B','C','D','E'], bipartite=0) # label one set of nodes "0"
B.add_nodes_from([1,2,3,4], bipartite=1) # label the second set of nodes "1"

B.add_edges_from([('A',1),('B',1),('C',1),('C',3),('D',2),('E',3),('E',4)])
```

Given a graph, we can do many operations related to bipartite graphs:
```python
# Check if a graph is bipartite
bipartite.is_bipartite(B)

# Check if a set of nodes is a bipartition of a graph (so one of the set in a bipartite graph)
X = set([1,2,3,4])
bipartite.is_bipartite_node_set(B,X)

# Get the two sets of bipartition
bipartite.sets(B)
```

THere are many interesting things we can understand from bipartite
graphs.
For example we may analyze one of the sets of the bipartite graph
to understand what are the affinities. This is done for example
for marketing purposes.

Let's say that one of the sets is represented by fans of a soccer team,
then, we can understand the affinities between these fans and provide
targeted advertisements.

In order to solve this we can study what are called the Projected Graphs.

## Projected Graphs

Projected graphs refer to the study of a specific set of a bipartite graph.

For example we can talk about **L-Bipartite Graph Projection** if we
consider the network of nodes in group L, where a pair
of nodes is connected if they have a common neighbor in R in the bipartite
graph.

We have a similar and specular definition for **R-Bipartite Graph Projection**,
which happens when we want to study the properties of the R set of nodes in
a bipartite graph.

Let's see how to work with these projection graphs using networkx:
```python
# Given a bipartite graph B we can do:
X = set(['A','B','C','D'])
P = bipartite.projected_graph(B,X)
# Taking the fan/soccer team example, this will give us the network of fans who have a team in common

# in this case we study the relationship among nodes A,B,C,D who belong
# to the L set

# We can also get the projected graph on the R set by specifying a different
# set of nodes
X = set([1,2,3,4])
P = bipartite.projected_graph(B,X)
# Taking the fan/soccer team example, this will give us a 
# network of teams who have a fan in common
```

Of course we can enrich these projection by getting **weighted projected graphs**.
An **L-Bipartite Weighted Graph Projection** is an L-Bipartite graph
projection with weights on the edges that are proportional to the number of
common neighbors between the nodes.

We can build a specular and similar definition for R-Bipartite Weighted Graph Projection.

In networkx we can do it like this:
```python
X = set([1,2,3,4])
P = bipartite.weighted_projected_graph(B,X)
```
