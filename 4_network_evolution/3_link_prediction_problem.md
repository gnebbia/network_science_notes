# The Link Prediction Problem

The network prediction problem is about understanding, given a fixed
network, how it is going to look in the future.

Among these problems we have the **link prediction problem** which is
about how we can predict which edges are going to be formed in the future.

These algorithms are used in many scenarios, for example, how do social
network provide recommendations about who can be your next friend and
so on.

So in this section we analyze different measure to understand
if given two nodes, they are likely to be connected in the future.

Some of the common measures we have to predict the likely of connection
between two nodes are:

- Common Neighbors
- Jaccard Coefficient
- Resource Allocation Index
- Adamic-Adar Index
- Preferential Attachment
- Community Common Neighbors    (Community Based)
- Community Resource Allocation (Community Based)

Note that none of these measures tell us whether or not
we should predict a particular edge is going to come up
in the future or not; but they just give us a score.
Also note that different measures can give us different
scores, leading to different rankings.

So basically what happens in general is that we use these measures
together as features and use a statistics/machine learning classifier
to perform the link prediction.
Or simply use some statistics such as mode or some normalized weighted
average for the ranking.


## Common Neighbors

The number of common neighbors of nodes X and Y is:
`comm_neigh(X,Y) = |N(X) intersection N(Y)|`
where:
- N(X) is the set of neighbors of node X
- N(Y) is the set of neighbors of node Y

In networkx we can compute this by doing:
```python
common_neigh = [(e[0],e[1], len(list(nx.common_neighbors(G,e[0],e[1])))) for e in nx.non_edges(G)]
# This returns a list of tuples which have the two nodes and the number of common neighbors
# and we are including only nodes which are not connected with each other
# since as we said we are interested in understanding what is the next link

# If we sort this list we can get the pairs of nodes most likely to connect
sorted(common_neigh,key=operator.itemgetter(2),reverse=True)
```

## Jaccard Coefficient

This measures takes the number of common neighbors of two nodes
and normalizes this number bu the total number of neighbors.
So the coefficient is computed as:
`jacc_coeff(X,Y) = (|N(X) intersection N(Y)|) / (|N(X) union N(Y)|)`
where:
- N(X) is the set of neighbors of node X
- N(Y) is the set of neighbors of node Y

In networkx we can compute this by doing:
```python
L = list(nx.jaccard_coefficient(G))
L.sort(key=operator.itemgetter(2),reverse=True)
print(L)
```

## Resource Allocation Index

The Resource Allocation Index measures the fraction of
a "resource" that a node can send to another node
through their common neighbors.
This value for two nodes X and Y is computed as:
`res_alloc(X,Y) = sum(1/|N(u)|) over all u in ( N(X) intersection of N(Y) )`
where:
- N(X) is the set of neighbors of node X
- N(Y) is the set of neighbors of node Y
- N(u) is the set of neighbors of node U which is a node in the intersection

So in this case if X and Y have a lot of common neighbors they are
going to have a large resource allocation index.
And if they have a lot of neighbors with a low degree they are going to have
even a larger resource allocation index.

This algorithm is based on the idea of each node distributing resources
to its neighbors, so if node X and Y share a set of neighbors who have
a low degree, it is more probable that resource allocation between these
nodes happens.

In networkx we can compute this by doing:
```python
L = list(nx.resource_allocation_index(G))
L.sort(key=operator.itemgetter(2),reverse=True)
print(L)
```

## Adamic-Adar Index

The Adamic-Adar Index measures the fraction of a "resource" that a node
can send to another node through their common neighbors.  It is very
similar to the resource allocation index, the only difference being
that instead of dividing by the degree of the common neighbors nodes,
we divide by the log of the degree.

This value for two nodes X and Y is computed as:
`adamic_adar(X,Y) = sum(1/log(|N(u)|)) over all u in ( N(X) intersection of N(Y) )`
where:
- N(X) is the set of neighbors of node X
- N(Y) is the set of neighbors of node Y
- N(u) is the set of neighbors of node U which is a node in the intersection

So in this case if X and Y have a lot of common neighbors they are
going to have a large Adamic-Adar index.
And if they have a lot of neighbors with a low degree they are going to have
even a larger Adamic-Adar index.

This algorithm is based on the idea of each node distributing resources
to its neighbors, so if node X and Y share a set of neighbors who have
a low degree, it is more probable that resource allocation between these
nodes happens.

In networkx we can compute this by doing:
```python
L = list(nx.adamic_adar_index(G))
L.sort(key=operator.itemgetter(2),reverse=True)
print(L)
```

## Preferential Attachment

The Preferential Attachment tells us that nodes with high degree
get more neighbors.
This is a very simple measure and it is just the product of
the degree of the two nodes.

This value for two nodes X and Y is computed as:
`pref_attach(X,Y) = |N(X)|*|N(Y)|`
where:
- N(X) is the set of neighbors of node X
- N(Y) is the set of neighbors of node Y


This algorithm is based on the idea behind the preferential attachment
model. So, high degree nodes are more likely to get more connections
with time.

In networkx we can compute this by doing:
```python
L = list(nx.preferential_attachment(G))
L.sort(key=operator.itemgetter(2),reverse=True)
print(L)
```

## Community Based Measures

Some measures take into account the concept of community structure
of the network for link prediction.

So for the following measures, let's assume that the nodes in the network
belong to different assigned communities (nodes can be people
and community can be departments of where the people is working).
A community is just a set of nodes.
Now in these contexts, we know that pairs of nodes who belong to the
same community and have many common neighbors in their community
are likely to form an edge.


## Community Common Neighbors

This measure is also called the "Common Neighbor Soundarajan-Hopcroft Score"
The number of common neighbors within the same commmunity of nodes X and Y
is rewarded, and this score is computed as:
`cn_sound_hop_score(X,Y) = |N(X) intersection N(Y)| + sum(f(u))`
where:
- N(X) is the set of neighbors of node X (in all the network, not depending on the community)
- N(Y) is the set of neighbors of node Y (in all the network, not depending on the community)
- f(u) is equal to 1 if u is in the same community as X and Y, or it is zero otherwise
- remember that u represents all the nodes in the intersection between X and Y

So basicallly f(u) is a bonus for belonging to the same community.

In networkx we can compute this by doing:
```python
# Notice that to compute this with networkx we first
# have to tell networkx to which community each node belongs to:
G.node['A']['community'] = 0
G.node['B']['community'] = 0
G.node['C']['community'] = 0
G.node['D']['community'] = 1
G.node['E']['community'] = 1
G.node['F']['community'] = 1
G.node['G']['community'] = 1
G.node['H']['community'] = 1

# Now we can compute this measure by doing:
L = list(nx.cn_soundarajan_hopcroft(G))
L.sort(key=operator.itemgetter(2),reverse=True)
print(L)
```

## Community Resource Allocation

This measure is also called the "Resource Alocation Soundarajan-Hopcroft Score"
and it is similar to the resource allocation index, but only considering
nodes within the same community.
This score is computed as:
`ra_sound_hop_score(X,Y) = sum( f(u) / |N(u)|')`
where:
- N(U)' is the set of neighbors of both X and Y which are in the same community as X and Y
- f(u) is equal to 1 if u is in the same community as X and Y, or it is zero otherwise
- remember that u represents all the nodes in the intersection between X and Y

Note that in this case if u is not within the same community of X and Y
that node u contributes 0 because of f(u) equal to zero in this case.

In networkx we can compute this by doing:
```python
# Notice that to compute this with networkx we first
# have to tell networkx to which community each node belongs to:
G.node['A']['community'] = 0
G.node['B']['community'] = 0
G.node['C']['community'] = 0
G.node['D']['community'] = 1
G.node['E']['community'] = 1
G.node['F']['community'] = 1
G.node['G']['community'] = 1
G.node['H']['community'] = 1

# Now we can compute this measure by doing:
L = list(nx.ra_soundarajan_hopcroft(G))
L.sort(key=operator.itemgetter(2),reverse=True)
print(L)
```
