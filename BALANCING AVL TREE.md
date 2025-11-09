# Experiment 10(e): AVL Tree - Left Rotation

## Aim
To write a Python function `def leftRotate(self, z)` to perform the left rotation operation in an AVL Tree. Additionally, insert '7' into the existing AVL Tree and perform the necessary rotations to balance it.

---

## Algorithm

1. Define the `TreeNode` class to represent each node in the AVL Tree with:
   - Key value
   - Left and right child pointers
   - Height of the node
2. Define the `AVL_Tree` class to manage AVL Tree operations.
3. In the `insert()` method:
   - Insert the key using Binary Search Tree (BST) logic.
   - Update the height of the current node.
   - Calculate the balance factor to check if the node is unbalanced.
   - Based on balance factor and key position, perform the necessary rotations (left or right).
4. Define the `leftRotate(z)` method:
   - Let `y = z.right` and `T2 = y.left`.
   - Make `z` the left child of `y`.
   - Assign `T2` as the right child of `z`.
   - Update the heights of `z` and `y`.
   - Return `y` as the new root of the subtree.
5. Insert the key '7' using the `insert()` method. If it causes an imbalance, perform the appropriate rotation.
6. Display the AVL Tree structure after insertion and rotations using preOrder traversal.

---

## Program

```

from TreeAVL.AVL import AVL

def getDictTree(self):
 return self.dict_tree

def Construct_AVL(L):
    tree = AVL(L)
    print("AVL Tree Before Balancing\n",getDictTree(tree))
    tree.BalanceTree()
    print("AVL Tree After Balancing\n", getDictTree(tree))
L=[11, 8, 18, 5, 13, 17, 4, 7, 2]
```

## OUTPUT
<img width="1260" height="152" alt="image" src="https://github.com/user-attachments/assets/636e530f-bbee-4e62-87e7-c4e0d1a3d477" />

## RESULT
Thus the Python program to construct an AVL tree, balance it, and print the nodes before and after balancing using the appropriate packages and built-in function was successfully executed.
