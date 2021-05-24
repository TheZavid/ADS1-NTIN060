# Algorithms and Data Structures.
Home assignment 11.

## *Task*:

Describe an algorithm which computes the number of inversions in a given permutation. The algorithm should work in time $\Theta(n\log n)$ where $n$ is the number of permuted integers. The permutation is given in an array $A[1\dots n]$ which consists of numbers $1,\dots,n$, for example $A=\{5,3,4,1,2\}$ is an array specifying a permutation of $n$ numbers. An inversion is defined as a pair of indices $1\leq i<j\leq n$ such that  A[i] > A[j] (i.e. A[i] and A[j] are in a wrong order). The number of inversions in the above example is 8.

## *Solution:*

Taking a hint that out algorithm should run in $\Theta(n\log n)$ into account, I conclude that I will use merge sort to get the desired number, but we don't actually want the sorting in this case. My idea is that I will have a global counter which will be incremented whenever element in the left sub array is greater then an element in the right sub array meaning that we have encountered the inversion.
Here is the pseudocode for the merge sort

```jsx
let n_inversions = 0

mergesort(array a)
	let n = len(a)
	if (n == 1)
		return a
	left_array = a[0]...a[n/2]
	right_array = a[n/2 + 1]...a[n]
	left_array = mergesort(left_array)
	right_array = mergesort(right_array)
	return merge(left_array, right_array)

merge(array a, array b)
	let c[len(a) + len(b)]
	
	while ( a and b are not empty)
		if (a[len(a)] > b[len(b)])
			add a[len(a)] to the end of c
			remove a[len(a)] from a
			// taking into account that inversion goes through all elements of b
			n_inversions += len(b)
		else
			add b[len(b)] to the end of c
			remove b[len(b)] from b

	while (a is not empty)
		add a[len(a)] to the end of c
		remove a[len(a)] from a
		
	while (b is not empty)
		add b[len(b)] to the end of c
		remove b[len(b)] from b
	
	return c	
```

When final merge sort returns $n\_inversions$ will contain the desired number.
As merge sort has time complexity of $\Theta(n\log{n})$, we will find the number of inversions in the same exact time.