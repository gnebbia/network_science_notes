# Hubs and Authorities

Hubs and authorities give other centrality measures to quantify importance
for nodes.

Note that these centrality measures are mostly used in the web domain
and search engines to quantify relevance of web pages (as it happens
with PageRank) but they can be applied to any network.

Hubs and authorities centrality measures are computed through an algorithm
called **HITS** which starts by constructing a set of relevant nodes
(we don't have the entire graph as with the PageRank technique) and
expand this set to a base set.  HITS then assigns an authority and a hub
score to each node in the network and applies rules similar to the ones
seen with PageRank where we have a number k of steps which will make
our authority and hub scores converge.  Nodes that have incoming edges
from good hubs are **good authorities** while nodes that have outgoing
edges to good authorities are **good hubs**.
NOTE: authority and hub scores converge for most networks.

We can use networkx to compute the hub and authority scores of
a network G like this:
```python
scores = nx.hits(G)
```

