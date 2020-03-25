# Node and Edge Attributes

## Attributes on Edges

```python
G.edges() # get a list of edges of the graph G
G.edges(data=True) # get edges with all their properties, sign, weight, etc...
G.edges(data='relation') # get all edges and outputs also the relationship without anything else
```

We can also access specific edges or specific attributes of certain
edges by doing:
```python
G.edge['A']['B'] # this gives the dictionary of attributes of edge (A, B)
G.edge['A']['B']['weight'] # this gives only the weight property of the edge (A, B)
```
In case of directed graphs, the order in which we specify nodes
matters.

In case of multigraphs we can get both the full dictionary
containing all relationships or a specific relantionship.
Let's see some examples:
```python
G = nx.MultiDiGraph()
G.add_edge('A','B',weight=6,relation='family')
G.add_edge('A','B',weight=18,relation='friend')
G.add_edge('C','B',weight=13,relation='friend')

# Now we can access edge attributes
# Access all relationships A->B
G.edge['A']['B']

# Access the attribute of a specific relationship
G.edge['A']['B'][0]['weight'] # this will get the weight of the first (0th) relationship between A and B
```

## Attributes on Nodes

We can also add attributes on nodes, let's see an example:
```python
G = nx.Graph()
G.add_edge('A','B',weight=6,relation='family')
G.add_edge('A','B',weight=18,relation='friend')

# Here we add additional properties to nodes
# the nodes can be existing (as in this case) or
# non existing
G.add_node('A',role='manager')
G.add_node('B',role='trader')
```

As with edges, we can query a list of nodes and also
output nodes with all their related data. Let's see
an example:
```python
# Retrieve all existing nodes
G.nodes()

# List all nodes with all their related attributes
G.nodes(data=True)
```

We can also access specific node attributes by doing:
```python
# get the attribute "role" for the node "A"
G.node['A']['role']
```

