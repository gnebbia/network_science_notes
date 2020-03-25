# PageRank Centrality

PageRank centrality is another centrality measure
developed by google founders to measure the importance
of webpages from the hyperlink network structure.

PageRank assigns a score of importance to each node.
Important nodes in this context are those with many
in-links from important pages.
(CIRCULAR DEFINITION? YES)

PageRank can be used for any type of network, but it
is mainly useful for directed networks.

Basically the algorithm here is:
n=number of nodes in the network
k=number of steps

1. assign all nodes a PageRank value of 1/n
2. perform the **Basic PageRank Update Rule** k times

The basic PageRank Update Rule is that each node gives
an equal share of its current pagerank to all the nodes
it links to.

Notice that with k increasing these value converge to a stable value,
so for k which goes to infinity we would get that converged value, but
generally just few iterations are enough to understand which is the most
important node.

Note that PageRank centrality is not similar to In-Degree centrality,
in fact, nodes with fewer in-degrees may have a high Page Rank when they
are connected to a more important node.

## Interpretation of PageRank Centrality Value

The PageRank centrality value of a node at step k is the probability
that a **random walker** on the graph lands on the node after taking k
steps.


## PageRank Loop Problem

Note that PageRank measures must solve the "PageRank Loop Problem", where
if we have a loop between two nodes, all the other nodes get a PageRank value
of 0 and only the two nodes in the loop get a value of 1/2.
So basically this happens everytime we have a network where very few nodes
suck up all the PageRank from the network.

In order to solve this problem we introduce the **damping parameter** alpha
and the concept of **Scaled PageRank**.
Basically we choose an outgoing edge at random and follow it to the next
node with probability "alpha".
And with probability "1-alpha" we choose a node at random and go to it.

What we're going to do now is that at every step, we're either going
to follow the edges with probability alpha.  Or we are going to forget
about the edges, and choose a random node, and go to it with probability
one minus alpha, and we're going to repeat this k times.

At this point we are no longer blocked on loops.
So basically the formula here to compute the PageRank changes a bit since
we have to take into account the damping factor.

Anyway we are not interested in the low level details, we just know that
this is called **Scaled PageRank** and is a good measure in the presence
of loops.

NOTE: Typical values for alpha are 0.8 or 0.9.

## Scaled PageRank

The **Scaled PageRank** of k steps and damping factor alpha of a node n
is the probability that a random walk with damping factor alpha lands
on n after k steps.

For most networks, as k gets larger, the scaled PageRank converges to
a unique value, which depends on alpha.


Note that the damping factor works better in very large networks like
when we want represent things like the web or large social networks.
Typical values for alpha are 0.8 or 0.9.

We can use the PageRank centrality measure in networkx by doing:
```python
# This computes the PageRank of network G with damping factor alpha
nx.pagerank(G,alpha=0.8)
```
