# Algorithms and Data Structures 1.
Home Assignment 13.

## *Task*:

A sorting algorithm based on comparisons needs at least $\lceil\log_25!\rceil=\lceil\log_2120\rceil=7$ comparisons to sort 5 numbers. Can you describe an algorithm which expects a quintuple and sorts it using at most 7 comparisons? Describe your algorithm in form of a decision tree.

## *Solution*:

Assuming a set $\{a,b,c,d,e\}$, We can provide the following algorithm (with $\dots$ denoting symmetric cases, as it would be rather tedious to write out the whole decision tree):

![Algorithms%20and%20Data%20Structures%202%20Home%20Assignment%201%209466c8a3cbee4966a723e16f046d43eb/method-draw-image_(1).svg](method-draw-image_(7).svg)

As we can see the sorting will complete in 7 comparisons.
