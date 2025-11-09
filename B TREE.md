# Experiment 10(c): B Tree

## Aim
To write a Python function `def insert(self, k)` to insert nodes in a B Tree.

---

## Algorithm

1. Start the program.
2. Define the `BTreeNode` class to represent a node with keys, children, and a leaf status.
3. Define the `BTree` class with methods to insert keys, handle node splits, and print the tree.
4. Implement the `insert()` method to insert a key into the tree, handling splits if necessary.
5. Implement the `insert_non_full()` method to insert a key into a node that is not full.
6. Implement the `split_child()` method to split a child node when it’s full.
7. Implement `print_tree()` to display the tree structure.
8. Run the program to insert keys and display the tree.
9. End the program.

---

## Program

```


class BTreeNode:
  def __init__(self, leaf=False):
    self.leaf = leaf
    self.keys = []
    self.child = []


# Tree
class BTree:
  def __init__(self, t):
    self.root = BTreeNode(True)
    self.t = t

    # Insert node
  def insert(self, k):
      root=self.root
      if len(root.keys)==(2*self.t)-1:
          temp=BTreeNode()
          self.root=temp
          temp.child.insert(0, root)
          self.split_child(temp,0)
          self.insert_non_full(temp, k)
      else:
          self.insert_non_full(root, k)

    # Insert nonfull
  def insert_non_full(self, x, k):
    i = len(x.keys) - 1
    if x.leaf:
      x.keys.append((None, None))
      while i >= 0 and k[0] < x.keys[i][0]:
        x.keys[i + 1] = x.keys[i]
        i -= 1
      x.keys[i + 1] = k
    else:
      while i >= 0 and k[0] < x.keys[i][0]:
        i -= 1
      i += 1
      if len(x.child[i].keys) == (2 * self.t) - 1:
        self.split_child(x, i)
        if k[0] > x.keys[i][0]:
          i += 1
      self.insert_non_full(x.child[i], k)

    # Split the child
  def split_child(self, x, i):
    t = self.t
    y = x.child[i]
    z = BTreeNode(y.leaf)
    x.child.insert(i + 1, z)
    x.keys.insert(i, y.keys[t - 1])
    z.keys = y.keys[t: (2 * t) - 1]
    y.keys = y.keys[0: t - 1]
    if not y.leaf:
      z.child = y.child[t: 2 * t]
      y.child = y.child[0: t - 1]

  # Print the tree
  def print_tree(self, x, l=0):
    print("Level ", l, " ", len(x.keys), end=":")
    for i in x.keys:
      print(i, end=" ")
    print()
    l += 1
    if len(x.child) > 0:
      for i in x.child:
        self.print_tree(i, l)

  

def main():
  B = BTree(3)

  for i in range(10):
    B.insert((i, 2 * i))
  print("B Tree :")
  B.print_tree(B.root)
  B.insert((11,))
  print("\nB Tree after insertion")
  B.print_tree(B.root)

if __name__ == '__main__':
  main()
```

## OUTPUT
<img width="1062" height="388" alt="image" src="https://github.com/user-attachments/assets/c1ebb324-5043-4f5e-90bc-1c9b790184f1" />


## RESULT
Thus the Python function def insert(self, key, value): to insert elements into a B Tree was written and executed successfully.
