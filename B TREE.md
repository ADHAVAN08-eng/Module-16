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

class Node(object):
    
    def __init__(self, order):
        
        self.order = order
        self.keys = []
        self.values = []
        self.leaf = True

    def add(self, key, value):
        
        if not self.keys:
            self.keys.append(key)
            self.values.append([value])
            return None

        for i, item in enumerate(self.keys):
            
            if key == item:
                self.values[i].append(value)
                break

            
            elif key < item:
                self.keys = self.keys[:i] + [key] + self.keys[i:]
                self.values = self.values[:i] + [[value]] + self.values[i:]
                break

        
            elif i + 1 == len(self.keys):
                self.keys.append(key)
                self.values.append([value])

    def split(self):
        
        left = Node(self.order)
        right = Node(self.order)
        mid = self.order // 2

        left.keys = self.keys[:mid]
        left.values = self.values[:mid]

        right.keys = self.keys[mid:]
        right.values = self.values[mid:]

      
        self.keys = [right.keys[0]]
        self.values = [left, right]
        self.leaf = False

    def is_full(self):
     
        return len(self.keys) == self.order

    def show(self, counter=0):
        
        print(counter, str(self.keys))

        
        if not self.leaf:
            for item in self.values:
                item.show(counter + 1)

class BPlusTree(object):
    
    def __init__(self, order=8):
        self.root = Node(order)

    def _find(self, node, key):
        
        for i, item in enumerate(node.keys):
            if key < item:
                return node.values[i], i

        return node.values[i + 1], i + 1

    def _merge(self, parent, child, index):
        
        parent.values.pop(index)
        pivot = child.keys[0]

        for i, item in enumerate(parent.keys):
            if pivot < item:
                parent.keys = parent.keys[:i] + [pivot] + parent.keys[i:]
                parent.values = parent.values[:i] + child.values + parent.values[i:]
                break

            elif i + 1 == len(parent.keys):
                parent.keys += [pivot]
                parent.values += child.values
                break

    def insert(self, key, value):
        parent=None
        child=self.root
        while not child.leaf:
            parent=child
            child,index=self._find(child,key)
        child.add(key,value)
        if child.is_full():
            child.split()
            if parent and not parent.is_full():
                self._merge(parent,child,index)
        
        # Write your code here

    def retrieve(self, key):
       
        child = self.root

        while not child.leaf:
            child, index = self._find(child, key)

        for i, item in enumerate(child.keys):
            if key == item:
                return child.values[i]

        return None

    def show(self):
        
        self.root.show()

def demo_node():
    node = Node(order=4)
    node.add('a', 'alpha')
    node.add('b', 'bravo')
    node.add('c', 'charlie')
    node.add('d', 'delta')
    node.show()

    print('\nSplitting node...')
    node.split()
    node.show()

def demo_bplustree():
    print('B+ tree...')
    bplustree = BPlusTree(order=4)
    x=input()
    y=input()
    bplustree.insert('a', 'alpha')
    bplustree.insert('b', 'bravo')
    bplustree.insert('c', 'charlie')
    bplustree.insert('d', 'delta')
    bplustree.insert('e', 'echo')
    # bplustree.insert('f', 'foxtrot')
    bplustree.insert(x,y)
    
    bplustree.show()

if __name__ == '__main__':
    demo_node()
    print('\n')
    demo_bplustree()
```

## OUTPUT
<img width="691" height="440" alt="image" src="https://github.com/user-attachments/assets/552e216d-71eb-4534-90cc-5881b9fa81eb" />

## RESULT
Thus the Python function def insert(self, key, value): to insert elements into a B+ Tree was written and executed successfully.
