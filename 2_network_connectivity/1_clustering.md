# Clustering Coefficient

Triadic Closure: Tendency for people who share connections in
a social network to become connected.
How can we measure the prevalence of triadic closure in a network?

NOTE: From here on we will refer to the term "friend" to mean
a node which is in relation with another node. So two connected nodes
are called "friends".

Another more general way to talk about triadic closure is **clustering**.

A **clustering coefficient** measures the degree to which nodes in a network
tend to "cluster" or form triangles.

We can measure clustering:
- from a node point of view -> Local Clustering Coefficient
- on a global network       -> Global Clustering Coefficient

## Local Clustering

Let's start with how we can measure clustering from the point of view
of a single node.  This type of clustering is known as the  **local
clustering coefficient of a node** and represents the fraction of pairs
of the node's friends that are friends with each other.

So the local clustering coefficient of a node C is computed as:
`# of pairs of C's friends who are friends / # of pairs of C's friends`.

So if C has 4 friends we can say that its **degree** is equal to 4.
Remember the **degree** is the number of connections a node has.

To compute the number of pairs or connections (friends) we can apply the
following formula:
`# of pairs of C's friends = (Dc*(Dc - 1))/ 2`
where Dc is the degree of C.
Note that this number represents all the possible unique pairs we can make
out of C's friends.

Now let's say that the `# of pairs of C's friends` is 6 and the
`# of pairs of C's friends who are friends` is 2 we can compute
the **Local clustering coefficient of C** by applying the above formula
and get `C=2/6=1/3`.


NOTE: Nodes who have less than 2 connections by definition have a local
clustering coefficient equal to zero.


We can compute the local clustering coefficient with networkx by doing:
```python
G = nx.Graph()
# Load graph data in some way
# ...
# Compute local clustering coefficient for the node 'F'
nx.clustering(G,'F')
```


## Global Clustering

Global clustering allows us to measure clustering on the whole network.

**Approach I**: Average local clustering coefficient over all nodes in
the graph. This approach to measure global clustering is called
**average local clustering** In networkx we can apply the approach I by doing:
```python
nx.average_clustering(G)
```

**Approach II**: Compute the percentage of open triads (i.e., open
triangles) in a network. Note that each triangle contains three open
triads (three nodes who form a path).
This second approach to measure global clustering is called
**Transitivity**. Transitivity is computed as:
`Transitivity = (3 * Number of closed triads) / number of open triads`
In networkx we can compute the transitivity by doing:
```python
nx.transitivity(G)
```

### Comparing Global Clustering Measures: Average Clustering vs Transitivity

So what are the differences between these two methods?
Both methods try to measure the tendency for the edges to form triangles.
But the main difference is in the fact that transitivity weights nodes
with large degree higher.
