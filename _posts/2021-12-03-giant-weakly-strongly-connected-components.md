---
layout: post
title: What is the difference between weakly strongly and giant connected components?
permalink: /weakly-strongly-connected-components/
published: true
date_readable:               Dec 03, 2021
last_modified_at_readable:   Dec 03, 2021
---

This post hopes to make a clear distinction between weak, strong and giant components, and I use the open-source code of [Gephi](https://gephi.org) to illustrate.

## The definition of a giant component is simply the connected component which has the largest number of nodes.

You can see it [in the code](https://github.com/gephi/gephi/blob/6e9096b69b8cf5e9dc7ad2e65ac8a80f269a5c33/modules/StatisticsPlugin/src/main/java/org/gephi/statistics/plugin/ConnectedComponents.java#L344
). The giant component of a graph (or network) is simply identified by:

- considering all the connected components,
- selecting the one that has the largest size (meaning, that has the most nodes)


## So, what is a "connected component"?

It depends whether your graph is directed or not. A graph is said to be _directed_ when the links (or connections, or edges) have a direction (A --> B : A is connected "in the direction of" B).
If the direction of the connection has no relevance (as in: A-B, there is no "direction" or "arrow" between A and B), the graph is said to be "undirected".

### if your graph is undirected:
A  connected component is used to mean a "_weakly_ connected component". In non technical terms, this is a group of nodes where no node is isolated, there is at least one connection linking a node to another.
See [this part of the code](https://github.com/gephi/gephi/blob/6e9096b69b8cf5e9dc7ad2e65ac8a80f269a5c33/modules/StatisticsPlugin/src/main/java/org/gephi/statistics/plugin/ConnectedComponents.java#L100
) which shows that weak components are computed when the graph is undirected.

### if your graph is directed:
 
 A connected component is used to mean a "strongly connected component", according to this definition: https://en.wikipedia.org/wiki/Strongly_connected_component.
 In non technical term, this is a group of nodes where it is possible to go from one node to any other node, even with taking into account that some links can be followed in just one direction.

 In the Gephi software, the method used to find these strongly connected components is [Tarjan's algorithm](https://en.wikipedia.org/wiki/Tarjan%27s_strongly_connected_components_algorithm
). The code for the tarjan's algorithm [is visible here](https://github.com/gephi/gephi/blob/6e9096b69b8cf5e9dc7ad2e65ac8a80f269a5c33/modules/StatisticsPlugin/src/main/java/org/gephi/statistics/plugin/ConnectedComponents.java#L253
).
 
 
