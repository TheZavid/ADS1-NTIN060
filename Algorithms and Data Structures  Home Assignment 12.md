# Algorithms and Data Structures 12.
Home Assignment.

## *Task:*

Professor Diogenes has $n$ supposedly identical integrated-circuit chips that in principle are capable of testing each other. The professor’s thest jig accommodates two chips at a time. When the jig is loaded, each chip tests the other and reports whether it is good or bad. A good chip always reports accurately whether the other chip is good or bad, but the professor cannot trust the answer of a bad chip. Thus the four possible outcomes of a test are as follows:

$\begin{array}{ccc}
\hline\\
\text{Chip A says}&\text{Chip B says}&\text{Conclusion}\\ \hline\\
\text{B is good}&\text{A is good}&\text{both are good, or both are bad}\\
\text{B is good}&\text{A is bad}&\text{at least one is bad}\\
\text{B is bad}&\text{A is good}&\text{at least one is bad}\\
\text{B is bad}&\text{A is bad}&\text{at least one is bad}\\ \hline
\end{array}$

(b) Consider the problem of finding a single good chip from among n chips, assuming that more than $\frac{n}2$ of the chips are good. Show that $\lfloor\frac{n}2\rfloor$ pairwise tests are sufficient to reduce the problem to one of nearly half the size.
(c) Show that the good chips can be identified with Θ(n) pairwise tests, assuming
that more than n/2 of the chips are good. Give and solve the recurrence that
describes the number of tests.

## *Solution:*

To solve part b we will split the initial $n$ chips into $\lfloor\frac{n}2\rfloor$ pairs among which we will perform the tests:
If both chips say that the other one is good we are going to take one form pair and put away the other, if otherwise we are going to put away both chips ( note that in this case we remove at least one bad chip for every good one we removed, so there still more good chips left then the bad ones). After all comparisons we are going to have at most $\lceil\frac{n}2\rceil$ chips left ( in the case where all pairs show "good, good" we just remove nearly the half of all chips).
To solve part c I will give the following recurrence of the algorithm described above:
$T(n)=T(\frac{n}2)+\Theta(n)$

As on each iteration of the algorithm we will reduce the problem into 1 sub problem half the size of the previous one and on each iteration we do $\frac{n}2$ comparisons, which with dropped constants results in time complexity of $\Theta(n)$.
Since $\log_2{1}=0<1=d$  time complexity of our algorithm is $T(n)=\Theta(n^d)=\Theta(n)$.
After the good chip is found we can find the rest of good chips conducting $n-1$ tests, which with dropped constants has time complexity of $\Theta(n)$.
Now summing up the time complexity of finding a single good chip and finding the rest of good chips knowing a single good chip we have: $\Theta(2n)=\Theta(n)$