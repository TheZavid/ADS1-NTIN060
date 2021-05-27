# Algorithms and Data Structures.
Home Assignment 8

## *Task*:

Suppose that the search for key $k$ in a binary search tree ends up in a leaf. Consider three sets: $A$, the keys to the left of the search path; $B$, the keys on the search path; and $C$, the keys to the right of the search path. Show (by giving a counterexample) that the following proposition is not true: Any $a\in A$, $b\in B$, and $c\in C$ must satisfy $a\le b\le c$.

## *Solution*:

Here is the counter example I have came up with:

![Algorithms%20and%20Data%20Structures%20Home%20Assignment%208%20467307606d4844368d09e01901eca36d/method-draw-image_(2).svg](method-draw-image_(2).svg)

On the picture the following sets:
$A=\{2\}$ on the left of the path

$B=\{5,10,7,6\}$ the path itself

$C=\{8\}$ on the right of the path

We have a counterexample for $a=2,b=10,c=8$ $(b>c)$.
Such situations happen when some nodes have only left subtree,  as we see on the picture, and the path ( starting from that node) goes only left. That way we are guaranteed to encounter (if any) a node in the set $C$ which is located in the left subtree of some node in $B$ which automaticaly makes its smaller.
