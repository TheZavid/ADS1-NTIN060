# Algorithms and Data Structures.
Home Assignment 7.

## *Task:*

Let us consider the following divide-and-conquer algorithm for computing minimum spanning trees: Given a graph $G=(V,E)$, partition the set $V$ of vertices into two sets $V_1$ and $V_2$ such that $|V_1|$ and $|V_2|$ differ by at most 1. Let $E_1$ be the set of edges that are incident only on vertices in $|V_1|$, and let $E_2$ be the set of edges that are incident only on vertices in $V_2$. Recursively solve a minimum spanning tree problem on each of the two subgraphs $G_1=(V_1,E_1)$ and $G_2=(V_2,E_2)$. Finally, select the minimum-weight edge in $E$ that crosses the cut $(V_1,V_2)$, and use this edge to unite the resulting two minimum spanning trees into a single spanning tree.
Either argue that the algorithm correctly computes a minimum spanning tree of $G$,
or provide an example for which the algorithm fails.

## *Solution:*

This algorithms has one major flaw. It doesn't specify how exactly vertices are split in two sets which is leading us to the fact that whether we will get a correct minimal spanning tree or not depends on our luck.
For example consider the following undirected weighted graph:

![Algorithms%20and%20Data%20Structures%20Home%20Assignment%207%204ef0b806a82c479993838bd4c21180f2/method-draw-image.svg](Algorithms%20and%20Data%20Structures%20Home%20Assignment%207%204ef0b806a82c479993838bd4c21180f2/method-draw-image.svg)

Lets proceed via the provided algorithm.
Suppose we split the vertices into two sets like this $V_1=\{u,t\},V_2=\{v,w\}$ which satisfies the conditions that sets differ in cardinality by at most 1, and our edges sets would be $E_1=\{(u,t)\},E_2=\{(v,w)\}$. As in each have we have only 2 vertices with 1 edge connecting them any spanning tree algorithm would have to choose that edge and those 2 vertices as a spanning tree. Next according to the algorithm we find the minimal-weight edges connecting that crosses the cut $(V_1,V_2)$ which is edge $(u,v)$ with weight 1. We get the resulting sum of edges in a spanning tree to be **11!** This is by no means correct as the actual minimal spanning tree of this graph has a total edge sum of **6!**
So we come to the conclusion that in its current form algorithm is not correct due to the randomness with which we partition the given graph.