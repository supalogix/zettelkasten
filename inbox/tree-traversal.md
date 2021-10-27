https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/

Algorithm Inorder(tree)
   1. Traverse the left subtree, i.e., call Inorder(left-subtree)
   2. Visit the root.
   3. Traverse the right subtree, i.e., call Inorder(right-subtree)
   
 Algorithm Preorder(tree)
   1. Visit the root.
   2. Traverse the left subtree, i.e., call Preorder(left-subtree)
   3. Traverse the right subtree, i.e., call Preorder(right-subtree) 

Algorithm Postorder(tree)
   1. Traverse the left subtree, i.e., call Postorder(left-subtree)
   2. Traverse the right subtree, i.e., call Postorder(right-subtree)
   3. Visit the root.

https://qr.ae/pGxklR

Pre-order traversal while duplicating nodes and values can make a complete duplicate of a binary tree. It can also be used to make a prefix expression (Polish notation) from expression trees: traverse the expression tree pre-orderly.
In-order traversal is very commonly used on binary search trees because it returns values from the underlying set in order, according to the comparator that set up the binary search tree (hence the name).
Post-order traversal while deleting or freeing nodes and values can delete or free an entire binary tree. It can also generate a postfix representation of a binary tree

https://qr.ae/pGxklU

Use of In-order:

In Binary Search Trees (Binary search tree) , to traverse through values in non-decreasing order.


In-Order Traversal will print values : 1 2 3 4 6 8 for the above binary search tree.

Use of Pre-Order:

Pre-order traversal is used to create a copy of the tree.

Pre-order traversal is also used to get prefix expression on of an expression tree. Please see http://en.wikipedia.org/wiki/Polish_notation to know why prefix expressions are useful.


Use of Post-Order :

Postorder traversal is used to delete the tree.

Postorder traversal is also useful to get the postfix expression of an expression tree. Please see http://en.wikipedia.org/wiki/Reverse_Polish_notation to for the usage of postfix expression.

https://softwareengineering.stackexchange.com/questions/186667/usefulness-of-pre-and-post-order-traversal-of-binary-trees

The point of having different algorithms to deal with binary trees is not to do things with trees. On this abstract level, one order is largely as good as any other, since you only get abstract symbols out of the procedure.

But trees are typically used to represent interesting stuff, and that can make a big difference in the outcome. For instance, if the nodes represent search states in a complete search through a big domain (maybe even an infinite domain), descending first vs. processing first not only determines in which order the results are found, it can even determine whether you will ever find any solutions at all. The point is easiest to see with infinite domains: if you descend incautiously, you might overlook a solution that lies quite high up in the tree, simply because you took a wrong turn. But in practice, since memory and disks are finite as well, this even applies to domains that are simply very large rather than truly infinite.

https://softwareengineering.stackexchange.com/questions/186667/usefulness-of-pre-and-post-order-traversal-of-binary-trees

The wikipedia article has a nice concise description of when you would want to use the different types of depth-first search:

Pre-order traversal while duplicating nodes and values can make a complete duplicate of a binary tree. It can also be used to make a prefix expression (Polish notation) from expression trees: traverse the expression tree pre-orderly.
In-order traversal is very commonly used on binary search trees because it returns values from the underlying set in order, according to the comparator that set up the binary search tree (hence the name).
Post-order traversal while deleting or freeing nodes and values can delete or free an entire binary tree. It can also generate a postfix representation of a binary tree.
It boils down to the logistical needs of an algorithm. For example, if you don't use post-order traversal during deletion, then you lose the references you need for deleting the child trees.
