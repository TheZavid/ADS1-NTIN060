# Algorithms and Data Structures.
Home assignment 9.

## *Task:*

Suppose that a node x is inserted into a red-black tree and then is immediately deleted, is the resulting red black tree the same as the initial red-black tree? Justify your answer

## *Solution:*

Since the process of inserting a node doesnt stop on just inserting a node, it also has to rebalance the tree. So we are going to have to look at the tree after rebalancing is performed which is very likely to change the tree, so the answer would be no for most cases.
See an example:

Initialy we have:

![Algorithms%20and%20Data%20Structures%20Home%20assignment%209%20a54f4a3547a146eea1668ec7872fcd33/method-draw-image_(4).svg](method-draw-image_(4).svg)

Lets insert 1:

![Algorithms%20and%20Data%20Structures%20Home%20assignment%209%20a54f4a3547a146eea1668ec7872fcd33/method-draw-image_(5).svg](method-draw-image_(5).svg)

Now delete 1:

![Algorithms%20and%20Data%20Structures%20Home%20assignment%209%20a54f4a3547a146eea1668ec7872fcd33/method-draw-image_(6).svg](method-draw-image_(6).svg)

As we see the resulting tree is not the same as before..
