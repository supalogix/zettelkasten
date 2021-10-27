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
