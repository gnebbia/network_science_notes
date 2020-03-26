# Preferential Attachment Model

We first have to define the **degree distribution**
that is the probability distribution of the degrees over the
entire network.

The degree distribution includes all the degrees characterizing
each node, so in a network with nodes A, B and C we will have:
P(A) = number of connections of node A / number of total nodes
P(B) = number of connections of node B / number of total nodes
P(C) = number of connections of node C / number of total nodes

We can plot the degree distribution of a network in networkx
in the following way:
```python
degrees = G.degree()
degree_values = sorted(set(degrees.values()))

histogram = [list(degrees.values()).count(i) / float(nx.number_of_nodes(G)) for i in degree_values]

import matplotlib.pyplot as plt
plt.bar(degree_values, histogram)
plt.xlabel('Degree')
plt.ylabel('Fraction of Nodes')
plt.show()
```


This works nicely in undirected networks, when we have directed networks
we have of course deal with in-degree or out-degree distribution.

Notice that in general, degree distributions for real-world graphs by
plotting on the x axis the degree and on the y axis the fraction of
nodes we can observe that these curves tend to follow a **power law**,
indeed they look like straight lines with endpoints in upper left and
lower right in a log-log scale.  A power law is a law of the type `P(k)
= Ck^(-alpha)`, where alpha and C are constants.

Note that models of network generation allow us to identify mechanisms
that give rise to observed patterns in real data.

Networks who follow the power law in simple terms are characterized
by the fact that most of the nodes in these network tend to have small
degree but only few nodes have very large degrees.
This is also called "the rich get richer" phenomena.

This phenomenon which characterizes many networks is explained by the
**Preferential Attachment Model** which describes how networks following
the power law may form mathematically.

Basically the Preferential Attachment Model allows us to create models
which generate networks who have a power law degree distribution.



## The Algorithm

- Start with two nodes connected by an adge
- At each step add a new node with an edge
  connecting it to an existing node at random with a certain probability
  P which is proportional to each node's degree
The probability P of connecting to a node u of degree ku is:
P(connecting to U) = ku / (sum(kj))
where sum(kj) is the sum of all other nodes' degrees.


As the number of nodes increases, the degree distribution of the
network under the preferential attachment model approaches the power law
`P(k) = Ck^(-3)` with constant C.

The preferential attachment model produces networks with degree distributions
very similar to real networks.

In networkx we can generate a network using the preferential attachment
model by doing:
```python
G_pa = nx.barabasi_albert_graph(n,m)
# This generates a network with n nodes
# and each new node attaches to m existing nodes according to the 
# Preferential Attachment model
```

We can also plot the degree distribution of our newly generated network
by doing:
```python
G = nx.barabasi_albert_graph(1000000,1)
degrees = G.degree()
degree_values = sorted(set(degrees.values()))

histogram = [list(degrees.values()).count(i) / float(nx.number_of_nodes(G)) for i in degree_values]

import matplotlib.pyplot as plt
plt.plot(degree_values,histogram,'o')
plt.xlabel('Degree')
plt.ylabel('Fraction of Nodes')
plt.xscale('log')
plt.yscale('log')
plt.show()
```
