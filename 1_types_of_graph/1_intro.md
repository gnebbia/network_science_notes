# Basic Definitions

## Networks

A network is a representation of connections among a set of items. The
items are called **nodes** (or vertices), and the inteconnections among
these items are called **edges** (or ties).

Networks are interesting since they are everywhere.


Let's see how to create netwoeks in networkx:
```python
import networkx as nx

G = nx.Graph()
G.add_edge('A','B')
G.add_edge('B','C')
...
```

### Directed and Undirected Networks

Relationships between nodes can either be:
- Symmetric (e.g., relatives);
- Asymmetric (e.g., what animal eats what);

Asymmetric relationships can be represented by undirected
edges, since the direction is not really important.
On the contrary, symmetric relationships can be represented
by directed edges.

In networkx we can create an undirected network by using
`G = nx.Graph()`, and we can create a directed network using
`G = nx.DiGraph()`.

### Weighted Networks

Note that not all relationships are equal, hence some edges carry higher
weight than others.  We can talk about **weighted network** when edges
are assigned a (typically numerical) weight.

In networkx we can represent weight by doing:
```python
G = nx.Graph()
G.add_edge('A','B',weight=6)
```


### Signed Networks

Some networks can carry information about friendshiip and antagonism
based on conflict or disagreement.

In these cases we can talk about **signed networks**.
A signed network is a network where edges are assigned positive
or negative sign.


In networkx we can represent sign by doing:
```python
G = nx.Graph()
G.add_edge('A','B',sign='+')
```

### Other edge attributes

Edges can carry many other labels or attributes,
so we can represent many different relationships
among vertices.
For example:
```python
G = nx.Graph()
G.add_edge('A','B',relation='friend')
```

### Multigraphs

**Multigraphs** are networks where a pair of nodes can have different types
of relationships simultaneously.

These are very flexible and general networks since we are able to
represent multiple relationships between nodes.  A multigraph is in
general a network where multiple edges can connect the same nodes
(parallel edges).

To create a multigraph in networkx we can do:
```python
G = nx.MultiGraph()
G.add_edge('A','B',relation='friend')
G.add_edge('A','B',relation='neighbor')
G.add_edge('A','B',relation='coworker')
```

We can also create directed multigraph by doing:
```python
G = nx.MultiDiGraph()
G.add_edge('A','B',relation='friend')
G.add_edge('A','B',relation='neighbor')
G.add_edge('B','A',relation='coworker')
```

### Choosing a graph type

So whenever we have to represent a domain, we can choose among these
parameters:
How many relationships can vertices have ?
- Normal Graph (1)
- MultiGraph (more than 1)

Does the direction of the relationship matter ?
- Directed Graph (direction)
- Undirected Graph (no direction)

Is the relationship characterized by a weight ?
- Weighted Graph (e.g., number of emails sent among employees,...)
- Not Weighted Graph (all relationships have the same importance/weight)

Can the relationship be classified as good/bad or positive/negative ?
- Signed Graph (for each relationship we will have a + or -)
- Not Signed Graph (all relationships are not charaacterized by a good/bad association)

Example:
We would like to construct a graph on NetworkX, where the nodes represent
employees of a company and the edges represent the number of times an
employee sent an email to another employee. What would be the best way
to represent this network?

Answer: In this case a possible choice would be a **weighted, directed graph**.
Since we want to capture who sent the email and who received it, we need
a directed graph. Since we also want to capture the number of times an
employee emailed another, we want the edges to have weights, hence we
want to use a weighted, directed graph.
