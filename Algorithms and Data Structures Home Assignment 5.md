# Algorithms and Data Structures.
Home Assignment 5.

### *Task:*

We are given a directed graph $G=(V,E)$ on which each edge $(u,v)\in E$ has an associated value $r(u,v)$, which is a real number in the range $0\leq r(u,v)\geq1$ that represents the reliability of a communication channel from vertex $u$ to vertex $v$. We interpret $r(u,v)$ as the probability that the channel from $u$ to $v$ will not fail, and we assume that these probabilities are independent. Give an efficient algorithm to find the most reliable path between two given vertices.

### *Solution*:

For this assignment I choose to use a modified version of  Dijkstra's Algorithm. Namely we would need to store an additional array of size $|V|$ to hold parent of a vertex from which shortest path comes from. Alternatively each vertex can represent a class which holds its children, current shortest distance and a parent from which the shortest path comes from. I would choose an option with an additional array as it seems to be more efficient in terms of memory usage.
We also have a problem connected to a fact that usually a Dijkstra's Algorithm finds a best path between given vertices as the smallest sum of edge weights between them. Assuming already having a working Dijkstra's Algorithm on hand it would be better to redefine edges weights to be more general. Lets proceed: we need to find a maximum $\prod r(u,v)$ between two given vertices this would be equivalent to finding a maximum $\log{\prod r(u,v)}$ since logarithm is an increasing function ( meaning as input increases output increases too ), we can rewrite that as $\sum{\log{r(u,v)}}$ according to a property of logarithm. That already look like the sum we are looking for but not quite as it gives negative values  in the interval $(0,1]$ and it would still require us to rewrite algorithm to find **longest** sum and we do not want that, so we multiply that by $-1$ and it beautifully translates into the smallest sum.
So the w function for this case would look like that:

```c
double
w(vertex u, vertex v)
{
	if (r(u,v) == 0) // as log is not defined at 0
		return infinity;
	else
		return -( log( r(u,v) ) );
}
```

The Dijkstra Algorithm can be modified according to specific requirements. For example:
If a graph G doesn't change and if we would need to also find the most reliable path to some other vertex in future it makes sense to construct the whole map.
If a graph G changes a lot or if we **only** need to find the most reliable path from a given vertex just once then there is no need to construct the whole map and we can halt Dijkstra's algorithm once we reach the required node as it means that the shortest path was found (it was chosen as a vertex with minimum distance so traversing other vertices would not yield a shorter distance)