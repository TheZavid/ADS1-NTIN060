# Algorithms and Data Structures:
HW2.

### *Task:*

Describe an algorithm which given an adjacency matrix $A$ of a directed graph $G=(V,E)$ finds out whether there is  a vertex $v\in V$ with indegree $|V-1|$ and outdegree $0$. The algorithm should have running time $O(|V|)$.

### *Solution:*

First I want to note that there could only be one such vertex because otherwise  there would be no way between these vertices hence no way to get $|V-1|$ indegree.
My plan is to do the following:
Traverse the adjacency matrix visiting each column exactly once. For example for this matrix:

$\def\arraystretch{1.3}
\begin{array}{c:c:c:c}
   0 & 0 & 1 & 1 \\ \hline
   0 & 1 & 1 & 1 \\ \hline
   1 & 0 & 0 & 1 \\ \hline
   0 & 0 & 0 & 0 \\
\end{array}$ 

Lets say we traverse this matrix starting at vertex 0 represented by the zero row. There are no edges $0\to0\text{ and }0\to1$ but there is an edge $0\to2$ so we jump to the vertex 2. At the vertex 2 we check if there is an edge $2\to3$ so we jump to vertex 3 and as we have reached the last column we stop. After that procedure we have ended up with one possible vertex that can satisfy our conditions, namely the vertex we have stopped at. That's due to the fact that If we have seen some vertex  and moved somewhere from it (0, 3) then it means it has an outdegree > 0, on the contrary if we have not visited some vertex (1) then it means that its missing at least one edge from some vertex (not including itself).
Now we only need to check if the vertex we have found satisfies our conditions. We will do it by checking the row that represents to which vertices the vertex leads and the column which represents which vertices lead to that vertex.

Here is the pseudocode of this algorithm:

```c
// adj_matrix[i][j] represents an adjacency matrix where i is a row and j is column
bool haveSpecial ( int[][] adj_matrix ){
		int n_v = len(adj_matrix[0]);
		int pos_v = 0; // vertex that might satisfy the conditions
		
		// this loop represents the procedure highlighted yellow in text
		// i.e. the traversal that finds possible vertex we need
		for ( int v = 0; v < n_v; v++ ){
				if ( adj_matrix[pos_v][v] == 1) 
						pos_v = v;
		}
		
		// this loop represents the procedure highlighted blue in text
		// i.e checks if the pos_v satisfies the conditions we need
		for ( int v = 0; v < n_v; v++ ){
				if ( adj_matrix[pos_v][v] != 0 || ( pos_v != v && adj_matrix[v][pos_v] != 1 ) )
							return false;
		}
	
		return true;
}
```

This algorithm has a running time $O(3|V|)$ as we need to look at maximum of $3|V|$ elements of the matrix to determine whether there is a vertex we need or not:
First we traverse the matrix $|V|$ times in order to find a matrix that might satisfy our conditions.
Then to check if the vertex we found indeed satisfies our conditions we need to check 1 row and 1 column which is $2|V|$ elements.
Dropping the constant we get running time $O(|V|)$ which is exactly what we need.

> By Ilia Zavidnyi