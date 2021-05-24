# Algorithms and Data Structures.
Home Assignment 6.

## *Task:*

Assume we are given a weighted graph $G=(V,E)$ with weights on
edges $d:E\to\Z$ and no negative cycles, and vertices $s,t\in V$. We want to find a
shortest path from $s$ to $t$ which moreover has the minimum number of edges among
all shortest paths (i.e. we are looking for a shortest path with the minimum number
of transfers). Describe an efficient algorithm to solve this problem.

## *Solution:*

This problem is great fit to use a Bellman-Ford algorithm since we need to find a shortest path in a weighted graph where weights of edges can be negative integers ( which immediately disqualifies Dijkstra algorithm ) and there can be no negative cycles.
The only issue we have here is that we have an additional parameter to determine favorable path. That is easily solved by introduction of a new parameter ( number of transfers ) and a modification of a Relax function:

```c
int ntrans[V] // an array holding V integer values for each vertex denoting
// the number of transfers in a shortest path to that vertex
// note that initialy all values should be 0

Relax (u, v, w):
	// note that with ntrans(u) + 1 means the transfer from u to v
	if ( d(v) == d(u) + w(u,v) && ntrans(v) > (ntrans(u) + 1) ) then
		p(v) = u
		ntrans(v) = ntrans(u) + 1
	else if ( d(v) > d(u) + w(u,v) ) then
		p(v) = u
		d(v) = d(u) + w(u,v)
		ntrans(v) = ntrans(u) + 1
	end if
```

Also there is no need to check whether there is a negative cycle in a graph with Bellman-Ford algorithms since we know that there would be no any.

The time complexity of a Bellman-Ford algorithm remains the same as we have only modified the Relax function so the time complexity is $\Theta(VE)$.