This is the last chapter of the book that discusses some algorithms and high level data structures.


Binary Search Trees

A Binary Search Tree is a hierarchical data structure that organizes sorted data in a tree-like fashion. It comprises nodes, each having a root node with two children nodes (left and right), and this pattern extends throughout the tree.

Key Properties

- The left child of a node must have a value less than the node.
- The right child of a node must have a value greater than the node.
- These conditions apply recursively to all nodes in the tree.

A binary search tree can be balanced or unbalanced, a balanced binary search tree has almost equal number of descendants on the left and right of the root node, whereas unbalanced binary search tree has an overwhelming number of descendants on the right or left.


Balanced Binary Search Tree

```
        5
       / \
      3   8
     / \ / \
    2  4 7  9

```

Search O(logn)

Insert O(logn)

Deletion O(logn)

Unbalanced Binary Search Tree

```
     1
      \
       2
        \
         3
          \
           4
            \
             5

```
Search O(n)

Insert O(n)

Deletion O(n)

<b>Implementation</b>

```python

class Node:
    def __init__(self, value, left=None, right=None):
        self.value = value
        self.left = left
        self.right = right

class Tree:
    def __init__(self, value=None):
        self.root = Node(value)
    
    def add_value(self, value):
        if self.root.value is not None:
            return self._rec_add(self.root, value)
        self.root = Node(value)
    
    def find_value(self, value):
        if self.root.value is not None:
            (parent, node) = self._find(None, self.root, value)
            return node
        return None

    def delete_node(self, value):
        (parent, node) = self._find(None, self.root, value)
        if node is None:
            return False

        # Case 1 --> The node is a leaf node
        if node.left is None and node.right is None:
            self._delete_child(parent, node, None)
            return True

        # Case 2 the node has just single child left or right, the other is None
        # assign the node value to the childs value.
        if node.left is not None and node.right is None:
            self._delete_child(parent, node, node.left)
            return True

        if node.right is not None and node.left is None:
            self._delete_child(parent, node, node.right)
            return True
 
        # Case 3 --> both left and right has value
        # Go to the right subtree of the node
        # recursively search the right subtree until you find the node with the minimum value.
        (parent, min_right_node) = self._find_leftmost(node, node.right)
    
        # take min_right_node value and replace it with the node value you want to delete
        node.value = min_right_node.value

        # if the min_right_node is a leaf node
        if min_right_node.right is None:
            self._delete_child(parent, min_right_node, None)
            return True
        
        # It has value
        parent.right = min_right_node.right
        return True
    
    def _delete_child(self, parent, child, new_child):
        if parent is None:
            self.root = new_child
        elif parent.left == child:
                parent.left = new_child
        elif parent.right == child:
            parent.right = new_child

    def _find_leftmost(self, parent, node):
            if node.left is None:
                return (parent, node)
            return self._find_leftmost(node, node.left)

    def _find(self, parent, node, value):
        if node is None:
            return None, None

        if node.value == value:
            return parent, node
            
        if node.value < value:
            return self._find(node, node.right, value)
    
        return self._find(node, node.left, value)

    def _rec_add(self, node, value):
        if value < node.value:
            if node.left is None:
                node.left = Node(value)
            else:
                return self._rec_add(node.left, value)
        else:
            if node.right is None:
                node.right = Node(value)
            else:
                return self._rec_add(node.right, value)
    def display_tree(self):
        self._display_tree_recursive(self.root, 0)
    
    def _display_tree_recursive(self, node, level):
        if node is not None:
            self._display_tree_recursive(node.right, level + 1)
            print("  " * level + str(node.value))
            self._display_tree_recursive(node.left, level + 1)

bst = Tree()
bst.add_value(10)
bst.add_value(6)
bst.add_value(29)
bst.add_value(4)
bst.add_value(2)
bst.add_value(30)
bst.add_value(7)
bst.add_value(20)
bst.display_tree()

print(bst.find_value(6))
print(bst.find_value(50))

print(bst.find_value(10))
bst.delete_node(10)
print(bst.find_value(10))
bst.display_tree()
bst.delete_node(4)
bst.display_tree()
  
```

More algorithms to explore
* More trees
    - Btrees
    - Heaps
    - Redblack trees
    - Splay trees
* Fourier Transforms
* mapReduce
* Bloom filters and hyperLogLog
* SHA algorigithms
    - Locality sensitive hashing
    - Diffie-Hellman key exchange
* Parallel algorithms
* Inverted Indexes
* Linear Programming 