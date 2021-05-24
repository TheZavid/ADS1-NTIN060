# Algorithms and Data Structures 1.
HW 3:

### *Tasks:*

Th diameter of an undirected tree $T=(V,E)$ is defined as as $max_{u,v\in V}\delta(u,v)$ where $\delta(u,v)$ denotes the longest path from $u$ to $v$ in $T$. Thus the diameter of $T$ is the maximum length of a path in $T$.  Describe a linear time algorithm which determines the diameter of a given tree $T$.

### *Solution:*

Trying to come up with solutions I've thought of two different approaches:

1. Choose a random node in a tree which will serve as root. Find the depth of each of its successors. Choose two max values from the received depths, sum them up and *voilà* we have the longest path in a tree since there can only be one path between every two nodes. That would run in $O(|V|)$ since we would have to traverse each branch of the root 2 times ( first inside it, then back to the root (in fact its a bit less then a multiple of 2 since we would see every leaf only one time)) and dropping the constants we get the linear time complexity.
2. As the task hints to use BFS I have came up with an idea that if we run the BFS 2 times we would find the the longest path. First run BFS at any node of a tree, the last visited node would be the furthest node lets call it  $u$. Then we run BFS at $u$, the last visited node would give us the longest path in a Tree considering we have been calculating weights. In this implementation we would visit each node exactly two times which is a bit less efficient then a former variant as we also visit every leaf 2 times dropping the constants we still get a linear time complexity $O(|V|)$

I will write the pseudocode for the second variant as I guess it what was expected:

```css
bfs_tree(tree, start)
{
	tree_distances = [-1] * |V| of tree; /* -1 represents not visited*/
	last_visited = start;
	queue.enqueue(start);
	cur_distance = 1;
	tree_distances[start] = 0;
	while queue not empty {
		u = queue.dequeue();
		foreach v successor of u {
			/*no need to check if we have already seen the node as it cannot occur in tree*/
			tree_distances[v] = cur_distance;
			queue.enqueue(v);
		}
		cur_distance += 1;
		last_visited = u;
	}
	return last_visited, cur_distance - 1; /*-1 from cur_distance because incremented on last iteration*/
}

find_diameter(tree)
{
	u, trash_dist = bfs_tree(tree, any_node);
	v, desired_dist = bfs_tree(tree, u);
	return desired_dist;
}
```

This algorithm runs in $O(|V|)$ as stated above due to the fact we conduct BFS twice and every BFS visits each node exactly once so the time complexity is $O(2|V|)$ dropping the constants we get the linear time complexity $O(|V|)$.