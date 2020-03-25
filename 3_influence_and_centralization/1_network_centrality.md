# Network Centrality

It is very important in a network to study the importance of nodes.
Based on the structure of a network, how can we know for example
which are the 5 most important nodes?


There are different ways to answer this question, some very basic examples are:
- Node Degree (number of edges);
- Node Average Proximity (how close it is to other nodes);
- Fraction of Shortest Paths passing by the node (how important it is for paths/communication);

These are just basic ideas on how to measure node importance.

We will be more precise in this section.
Let's start from some definition, "how important" is more precisely
called **network centrality** in network science.  This is particularly
interesting in real-world applications since it allows us to perform
multiple tasks, some examples are related to finding out:
- who are influential nodes in a social network;
- nodes that disseminate information to many nodes or prevent epidemics;
- hubs in a transportation network;
- important pages on the web;
- nodes that prevent the network from breaking up;

There are different **centrality measures**, some of the most important
are:
- Degree centrality;
- Closeness centrality;
- Betweenness centrality;
- Load centrality;
- Page rank;
- Katz centrality;
- Percolation centrality;


## Notes on Centrality Measures

Note that applying different centrality measures would produce
different rankings. This is totally normal and happens because each
measure has a different definition for the concept of "importance",
and make different assumptions about what it means to be a "central"
node. Anyway, generally we want to pick the measure which has the
definition of importance/centrality we are more interested in or more
compatible with our interests.  The best centrality measure indeed
depends on the context of the network we are analyzing.

Sometimes, we simply have no preference about the importance
definition or we are interested in more importance measures, that's why
it may be a good idea to use more centrality measures and find the most
frequent instead of relying on a single one.
