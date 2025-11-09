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


class TreeNode(object):
	def __init__(self, val):
		self.val = val
		self.left = None
		self.right = None
		self.height = 1

class AVL_Tree(object):
	def insert(self, root, key):
		if not root:
			return TreeNode(key)
		elif key < root.val:
			root.left = self.insert(root.left, key)
		else:
			root.right = self.insert(root.right, key)

	
		root.height = 1 + max(self.getHeight(root.left),
						self.getHeight(root.right))

		balance = self.getBalance(root)

		if balance > 1 and key < root.left.val:
			return self.rightRotate(root)

	
		if balance < -1 and key > root.right.val:
			return self.leftRotate(root)

		
		if balance > 1 and key > root.left.val:
			root.left = self.leftRotate(root.left)
			return self.rightRotate(root)
   
		if balance < -1 and key < root.right.val:
			root.right = self.rightRotate(root.right)
			return self.leftRotate(root)

		return root

	def leftRotate(self, z):
	    y=z.right
	    t2=y.left
	    
	    y.left=z
	    z.right=t2
	    
	    z.height=1+max(self.getHeight(z.left), self.getHeight(z.right))
	    y.height=1+max(self.getHeight(y.left), self.getHeight(y.right))
	    return y

	def getHeight(self, root):
		if not root:
			return 0

		return root.height

	def getBalance(self, root):
		if not root:
			return 0

		return self.getHeight(root.left) - self.getHeight(root.right)

	def preOrder(self, root):

		if not root:
			return

		print("{0} ".format(root.val), end="")
		self.preOrder(root.left)
		self.preOrder(root.right)


myTree = AVL_Tree()
root = None

n=int(input())
root = myTree.insert(root, 13)
root = myTree.insert(root, 10)
root = myTree.insert(root, 15)
root = myTree.insert(root, 5)
root = myTree.insert(root, 11)
root = myTree.insert(root, 16)
root = myTree.insert(root, n)

print("Preorder traversal of the constructed AVL tree is")
myTree.preOrder(root)
print()

```

## OUTPUT
<img width="1092" height="240" alt="image" src="https://github.com/user-attachments/assets/7884fd50-d36c-4634-a15a-8d4cc58889c8" />


## RESULT
Thus the Python function def leftRotate(self, z): to perform the left rotation operation in an AVL Tree and insert the element '7' into it was executed successfully
