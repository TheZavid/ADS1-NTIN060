# Algorithms and Data Structures
HW 4:

### *Task:*

We say that a directed graph $G=(V,E)$ is half-connected if for every
pair of vertices $u,v\in V$ there is a directed path from $u$ to $v$ or from $v$ to $u$ (or both).
Describe an algorithm which determines whether a given directed graph is half-connected

### *Solution:*

That task would have been simple if we were given an acyclic graph since in this case we could have just run a DFS which gradually "removes" vertices from the graph and checks on very iteration whether more then 1 vertices have a zero indegree in which case the graph is not half-connected  as multiple nodes with 0 indegree are unreachable (don't have a directed path between them) from each other in directed acyclic graph.
We will keep that part of the solution. However we first need to eliminate cycles. We will do it by creating a graph $G'=(V',E')$ where $V'$  is a set of strongly connected component of $G$ and $E'$ represent an edge between the connected components (which occurs when any element of one connected component is connected to any element of another).
We will find connected components using a Korasaju's algorithm which consist of two DFS and one construction of a transposed graph which overall gives  a time complexity of $\Theta(V+E)$.

Here is the pseudocode for the solution:

```python
# recursive DFS which leaves with with a stack of verticies sorted by decresing
# discovery time
func fillStack(v, stack, visited) {
	visited[v] = true;
	foreach edge (v, u) in G {
		if visited[u] == false
			fillStack(u, stack, visited);
	}
	stack.push(v);
}

func reverse(graph G) -> graph GT {
	graph GC with vertices of G;
	foreach v in G {
		foreach edge (v,u) in G {
			add edge (u,v) to GC;
		}
	}
	return GT;
}

func findSCC(v, visited) -> SCC{
	visited[v] = true;
	component SCC += v;
	foreach edge (v, u) in GT {
		if visited[u] == false
			SCC += findSCC(u, visited);
	}
	return SCC;
}

func korasaju(graph G) -> graph GC {
	stack;
	bool[] visited = [false] * vertices of G;
	foreach v in G {
		if visited[v] == false
			fillStack(v, stack, visited)
	}
	
	# init visited back to zero
	visited = [false] * vertices of G;

	GT = reverse(G);

	graph GC;
	
	# create GC from connected components of GT
	while stack non empty {
		v = stack.pop();
		
		if visited[v] == false 
			add findSCC(v) as vertex to GC;
	}
	
	return GC;
	
}

func isHalfConnected(graph G) -> bool {
	# get connected component graph of G
	graph GC = korasaju(G);
	int[] indegree = [0] * vertices of GC
	
	# compute indegrees of vertices of GC
	foreach v in GC {
		foreach edge (u,v) in G
			indegree[v] += 1;
	}
	
	root = Null;
	# find vertex with indegree 0 if more then 1 return false
	foreach v in GC {
		if indegree[v] == 0 {
			if root != Null
				return false;
			else
				root = v;
		}
	}
	
	# delete vertices until we reach a vertex with outdegree 0
	# if encounter multiple 0 indegree vertices return false
	while root != Null {
		next = Null;
		foreach (root, u) in GC {
			indegree[u] -= 1;
			if indegree[u] == 0 {
				if next != Null
					return false;
				else
					next = u;
			}
		}
		
		root = next;
	}
	
	return true;
}
```

Let us count a time complexity of  this solution as we already know the Korasaju's algorithms running time is $\Theta(V+E)$ due to the fact getting a transposed graph have a constant running time.  isHalfConnected function also runs in constant time $\Theta(V+E)$ due to the fact that we always need to calculate indegrees  which takes constant time + the rest of the program which takes (dropping constants) $O(V+E)$, the sum results in exactly $\Theta(V+E)$. Adding time complexity of Korasaju's algorithm and IsHalfConnected function we once again get $\Theta(V+E)$