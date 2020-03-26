# Small World Networks

This model is the one behind the "Six degrees of separation" which
states that also in very large networks what happen is that we can reach
any other node in median with relatively short paths.  In different
experiments depending on the data the average path was 5,6 or 7.
In general these large networks with these short paths are characterized
by large local clustering coefficients.  This takes us to the conclusion
that social networks tend to have high clustering coefficient and small
average path length.

So scientists searched a generative model which have these two properties,
hence, large clustering coefficients and small average path lengths.
The answer is given by the **Small World Model**.

But first, let's analyze why the Preferential Attachment model does
not perform good in these contexts.

Unluckily the Preferential Attachment model is not very good in these
social network scenarios since it tends to create networks with an
average clustering coefficient decreasing with the number of nodes
increasing. Anyway the preferential attachment model produces graphs
with short average path length.
So why the preferential attachment model does not do good with
clustering coefficient?  It is because it has no mechanism to favor
triangle formation.

The **small world model** is able to generate networks with high
clustering coefficient and small average shortest paths.

The degree distribution of small world network is not a power law because
the degree of most nodes lie in the middle.

## The Algorithm

Let's see how the small world model algorithm works:
- Start with a ring of n nodes, where each node is connected to its
  k nearest neighbors;
- Fix a parameter p which is in the interval [0,1];
- Consider each edge (u,v) and with probability p, select a node w at
  random and rewire the edge (u,v) so that it becocmes (u,w);
  (Do this for each of the edges)

Typical values for k are values larger than 2 (from 4 to 8)
and the probability p is generally kept low, between 0 (excluded) and 0.1
(e.g., 0.04).

In networkx we can generate networks using the small world model by
doing:
```python
G = nx.watts_strogatz_graph(n,k,p)
# This returns a small world network with n nodes, starting
# with a ring lattice with each node connected to its k nearest neighbors
# and rewiring probability p
```

We can also plot the network degree distribution by doing:
```python
G = nx.watts_strogatz_graph(n,k,p)
degree_values = sorted(set(degrees.values()))

histogram = [list(degrees.values()).count(i) / float(nx.number_of_nodes(G)) for i in degree_values]

import matplotlib.pyplot as plt
plt.bar(degree_values, histogram)
plt.xlabel('Degree')
plt.ylabel('Fraction of Nodes')
plt.show()
```


### Explanation of the parameter p

But let's see how do these networks change by changing the p probability
of rewiring parameter.
With:
- p=0, we have what is called a **regular network** with high local
  clustering coefficients, but with large networks, the distances between nodes
  can get very large;
- p=1, we have what is called a **random network** where alle edges are rewired
  so basically we obtain a random network with a small local
  clustering coefficient but with short distances between nodes;
- p between 0 and 1, we have what is called a **small world network** with 
  high local clustering coefficients, and with short distances between nodes.
  This last option is the best of both world since it keeps short distances
  thanks to some rewiring but a high clustering coefficient thanks to the
  initial structure given to the network, and this is the reason to use p
  to build small world model generated networks.

## Small World Model and Disconnected Networks

Note that the small world model may give us a disconnected network
as result in its generative process. This happens because of the rewiring
involved in the process.

Anyway if we want to not have a disconnected network with different connected
components we can rerun the algorithm t times until the result is a fully
connected network.

In networkx this can be done in this way:
```python
G = nx.connected_watts_strogatz_graph(n,k,p,t)
# This method runs watts_strogats_graph(n,k,p) up to t times
# until it returns a connected small world network
```

## Small World Model Variation (Newman-Watts-Strogatz Model)

There is a variation on the small world model which is called
Newman-Watts-Strogatz model which runs a very similar algorithm to the
small world model, but rather than rewiring edges, it adds new edges
with probability p.

In networkx we can generate networks using these model by doing:
```python
G = nx.newman_watts_strogatz_graph(n,k,p)
```
