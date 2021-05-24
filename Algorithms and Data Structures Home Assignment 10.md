# Algorithms and Data Structures.
Home Assignment 10.

## *Task:*

Let us consider two arrays $X$ and $Y$ of $n$ integers each. Let us assume that the arrays are sorted (say in increasing order). Describe an algorithm which finds the median of all $2n$ numbers in both arrays. The algorithm should work in time $O(\log n)$.

## *Solution:*

Such task can be easily done by merging two arrays and finding the median from there, but that would run in $O(n)$ which is not what we need.
As the task suggest by itself we would need to split the working arrays into workable part, ***Divide et Empera.***

I will take advantage of the fact that two given arrays are sorted. First we will take a look at the median of both arrays, if its the same we can immediately return so our best case running time is $\Omega(1)$. However we are not always going to be that lucky, if median of $X$ is greater then the median of $Y$ then we would divide them in half and look for a median in the first half of $X$ ( we need elements smaller then median) and the second half of $Y$( we need elements greater then median) and for the case when median of $X$ is smaller rules are reversed. In case we have not found median and we have reduced both arrays to the size of 2, we will get two middle elements as if we have merged them by choosing the greatest of the first elements in both arrays adding to it the least of second elements of both arrays and dividing by two.
Here is the pseudocode for such algorithm:

```c
int
median ( int[] A )
{
	int index = sizeof (A) / 2;
	if (sizeof (A) % 2 == 0)
		return (A[index-1] + A[index]) / 2;
	else
		return A[index];
}

int
find_median( int[] X, int[] Y )
{
	int sizeX = sizeof (X);
	int sizeY = sizeof (Y);
	if ( sizeX == 2 && sizeY == 2)
		return (max(X[0], Y[0]) + min(X[1], Y[1])) / 2; // red highlight
	int medX = median(X);
	int medY = median(Y);
	if ( medX == medY )
		return medX; // green highlight
	else if ( medX > medY )
		return (find_median( X[0, sizeX/2], Y[sizeY/2, sizeY-1] ); // yellow highlight
	else
		return (find_median( X[sizeX/2, sizeX-1], Y[0, sizeY/2] );
}
```