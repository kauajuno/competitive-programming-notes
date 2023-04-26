# What are trees?

Trees are Data Structures which can organize data in a way that makes it easy to search and navigate through them.

![[basic-tree-structure.png]]

Some key concepts to understand trees are:

- Node: each element in the tree is known as a node.
- Links/Edges: relationships between the nodes.
- Root: the node at the top of the tree (in an analogy to the real world trees, this data structure is like an upside-down real world tree). In the image above, A is the root.
- Parent: a node which comes right before another one.
- Child: a node which comes right after before another one.
- Siblings: nodes with the same parent.
- Leaf: a node which has no children.
- Ancestor: a node that comes somewhere before another one.
- Descendant: a node that comes somewhere after another one.

# Recursive definition

Trees can be defined recursively if we think that each node that comes after the root is also a root to their own sub-trees. This goes on and on until the leaves are reached. With this definition it is also possible to state that a tree might be composed of a single node.
That being said, an important property of the trees is that they're always having $n$ nodes and $n-1$ edges.

# Depth and Height

Depth can be defined as the size of the path from the root to a specific node, while height is defined as the size of the longest path from a specific node to a leaf. Let's see an example:

![[depth-height-tree-ds.png]]

Node 5 has a **depth of 2 and a height of 1**, because there are two edges between node 5 and the root and one edge between 5 and the farest leaf (both nodes 9 and 10).
Node 3 has a **depth of 1 and a height of 2**, because node 3 is a straight up child of the root and the farest leaf is the node 11, which is two edges away.

> [!info]
> The height of a tree is defined as the height of the root node.

# Application of trees

Trees have four main applications:

- Storing hierarchically (file systems)
- Organize data
- Tries
- Network routing algorithms

# Types and subdefinitions of trees

- [[Binary Trees]]
- [[Tries]]
- 

---

#datastructures