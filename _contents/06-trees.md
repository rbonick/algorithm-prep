---
title: Trees
---
## Trees
Tree properties:
* Full - either 0 or 2 children (no single leaves)
* Complete - completely filled tree, with possible exception of lowest depth, which is filled from left to right
* Balanced - depth of leaves does not exceed a particular amount

#### Binary Search Tree
Binary tree (2 children) where the following property always holds:

Let *x* be a node in a binary search tree. If *y* is a node in the left subtree
of *x*, then *y.key* <= *x.key*. If *y* is a node in the right subtree of *x*,
then *y.key* >= *x.key*.

###### Searching
```
find(root, key){
    if(root == null || root.value == key){
        return root;
    }
    if(key <= root.value){
        return find(root.left, key);
    } else {
        return find(root.right, key);
    }
}
```

###### Insertion
```
insert(root, node){
    current = root;
    insertionSpot = null;
    while(current != null){
        insertionSpot = current;
        if(node.value <= current.value){
            current = current.left;
        } else {
            current = current.right;
        }
    }
    if(insertionSpot == null){
        root = node;
    } else if(node.value <= insertionSpot.value){
        insertionSpot.left = node;
    } else {
        insertionSpot.right = node;
    }
    return root;
}
```

###### Deletion
```
delete(root, node){
    if(node.left == null){ // nothing on the left, so we can transplant the right child without concerns
        transplant(root, node, node.right);
    } else if (node.right == null){ // nothing on the right, so we can transplant the left child without concerns
        transplant(root, node, node.left);
    } else {
        replacement = successor(node); // find successive element, which is the leftmost node in the right subtree
        if(replacement.parent != node){
            // Replacement will be taking the spot of the node, but its right child needs to take its spot
            transplant(root, replacement, replacement.right); // replace the replacement with its right element to keep the BST intact
            replacement.right = node.right;
            replacement.right.parent = replacement;
        } else {
            transplant(root, node, replacement);
            replacement.left = node.left;
            replacement.left.parent = replacement;
        }
    }
}

transplant(root, uproot, replacement){
    if(uproot.parent == null){ // uprooting the root
        root = replacement;
    } else if (uproot == uproot.parent.left){
        uproot.parent.left = replacement;
    } else {
        uproot.parent.right = replacement;
    }
    if(replacement != null){
        replacement.parent = uproot.parent;
    }
    return root;
}
```

#### Red-Black Trees
A red-black tree is a binary tree with an extra `color` field that satisfies the following criteria:
* Every node is either red or black
* The root is black
* Every leaf is
* If a node is red, then both children are black
* All straight paths from the node to its leaves contains the same number of black nodes

###### Rotations
Since the red-black criteria must be preserved, Oftentimes
we have to rotate the a particular node right or left.

```
Rotating left (X)
    X                       Y
   / \                     / \
  A   Y       -->         X   C
     / \                 / \
    B   C               A   B

leftRotate(root, node){
    rotateTarget = node.right;

    // Turn rotate target's left subtree into node's right subtree
    node.right = rotateTarget.left;
    if (rotateTarget.left != null){
        rotateTarget.left.parent = node;
    }

    // link node's parent to rotate target
    rotateTarget.parent = node.parent;
    if(node.parent == null){
        root = rotateTarget;
    } else if (node == node.parent.left){
        node.parent.left = rotateTarget;
    } else {
        node.parent.right = rotateTarget;
    }

    // put node on rotate target's left
    rotateTarget.left = node;
    node.parent = rotateTarget;

    return root;
}
```

```
Rotating right (Y)
     Y                      X
    / \                    / \
   X   C      ->          A   Y
  / \                        / \
 A   B

rightRotate(root, node){
 rotateTarget = node.left;

 // Turn rotate target's right subtree into node's left subtree
 node.left = rotateTarget.right;
 if (rotateTarget.right != null){
     rotateTarget.right.parent = node;
 }

 // link node's parent to rotate target
 rotateTarget.parent = node.parent;
 if(node.parent == null){
     root = rotateTarget;
 } else if (node == node.parent.left){
     node.parent.left = rotateTarget;
 } else {
     node.parent.right = rotateTarget;
 }

 // put node on rotate target's right
 rotateTarget.right = node;
 node.parent = rotateTarget;

 return root;
}
```

###### Insertions
```
insert(root, node){
    insertPoint = null;
    currentNode = root;
    while(currentNode != null){
        insertPoint = currentNode;
        if(node.value <= currentNode.value){
            currentNode = currentNode.left;
        } else {
            currentNode = currentNode.right;
        }
    }

    node.parent = insertPoint;
    if(insertPoint == null){
        root = insertPoint;
    } else if (node.value <= insertPoint.value){
        insertPoint.left = node;
    } else {
        insertPoint.right = node;
    }

    node.color = red;

    insertFixup(root, node);

    return root;
}

insertFixup(root, node){
    while(node.parent.color == red){
        if(node.parent == node.parent.parent.left){
            uncle = node.parent.parent.right;
            if(uncle.color == red){
                node.parent.color = black;
                uncle.color = black;
                node.parent.parent.color = red;
                node = node.parent.parent;
            } else if (node == node.parent.right){
                node = node.parent;
                leftRotate(root, node);
            } else {
                node.parent.color = black;
                node.parent.parent.color = red;
                rightRotate(root, node.parent.parent);
            }
        } else {
            uncle = node.parent.parent.left;
            if(uncle.color == red){
                node.parent.color = black;
                uncle.color = black;
                node.parent.parent.color = red;
                node = node.parent.parent;
            } else if (node == node.parent.left){
                node = node.parent;
                rightRotate(root, node)
            } else {
                node.parent.color = black;
                node.parent.parent.color = red;
                leftRotate(root, node.parent.parent);
            }
        }
    }
    root.color = black;
}
```

###### Deletions
```
transplant(root, node, replacement){
    if(node.parent == null){
        root = replacement;
    } else if (node == node.parent.left){
        node.parent.left = replacement;
    } else {
        node.parent.right = replacement;
    }
    replacement.parent = node.parent;
    return root;
}

delete(root, node){
    deleteOrMovedNode = node;
    originalColor = deleteOrMovedNode.color;

    if(node.left == null){
        replacement = node.right;
        transplant(root, node, node.right);
    } else if (node.right == null){
        replacement = node.left;
        transplant(root, node, node.left);
    } else {
        deleteOrMovedNode = treeMinimum(node.right);
        originalColor = deleteOrMovedNode;

        replacement = deleteOrMovedNode.right;
        if(deleteOrMovedNode.parent == node){
            replacement.parent = deleteOrMovedNode;
        } else {
            transplant(root, deleteOrMovedNode, deleteOrMovedNode.right);
            deleteOrMovedNode.right = node.right;
            deleteOrMovedNode.right.parent = deleteOrMovedNode;
        }

        transplant(root, node, deleteOrMovedNode);
        deleteOrMovedNode.left = node.left;
        deleteOrMovedNode.left.parent = deleteOrMovedNode;
        deleteOrMovedNode.color = node.color;
    }

    if(originalColor == black){
        deleteFixup(root, replacement);
    }
}

deleteFixup(root, node){
    while(node != root && node.color == black){
        if(node == node.parent.left){
            sibling = node.parent.right;

            if(sibling.color == red){
                sibling.color = black;
                node.parent.color = red;
                leftRotate(root, node.parent);
                sibling = node.parent.right;
            }

            if(sibling.left.color == black && sibling.right.color == black){
                sibling.color = red;
                node = node.parent;
            } else if (sibling.right.color == black){
                sibling.left.color = black;
                sibling.color = red;
                rightRotate(root, sibling);
                sibling = node.parent.right;
            }

            sibling.color = node.parent.color;
            node.parent.color = black;
            sibling.right.color = black;
            leftRotate(root, node.parent);
            node = root;
        } else {
            sibling = node.parent.left;

            if(sibling.color == red){
                sibling.color = black;
                node.parent.color = red;
                rightRotate(root, node.parent);
                sibling = node.parent.left;
            }

            if(sibling.right.color == black && sibling.left.color == black){
                sibling.color = red;
                node = node.parent;
            } else if (sibling.left.color == black){
                sibling.right.color = black;
                sibling.color = red;
                leftRotate(root, sibling);
                sibling = node.parent.left;
            }

            sibling.color = node.parent.color;
            node.parent.color = black;
            sibling.left.color = black;
            rightRotate(root, node.parent);
            node = root;
        }
    }
}
```
