# Experiment 10(d): B+ Tree

## Aim
To write a Python function `def insert(self, k)` to insert nodes in a B+ Tree.

---

## Algorithm

1. Define the `Node` class to represent a node in the B+ Tree with keys, values, and methods for adding keys, splitting the node, checking if it's full, and showing its contents.
2. Define the `BPlusTree` class to represent the entire B+ Tree with methods to find, insert, retrieve, and merge nodes, and display the tree.
3. In the `insert()` method, insert a key-value pair into the tree, and split nodes if necessary while merging them when they become full.
4. In the `retrieve()` method, search for a key in the tree and return its associated values.
5. Call `demo_node()` and `demo_bplustree()` to demonstrate the creation, insertion, and splitting of nodes in the tree and show the structure of the B+ Tree.

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
<img width="691" height="440" alt="image" src="https://github.com/user-attachments/assets/423c323c-7a8c-4375-ac67-6d87ffd49a57" />

## RESULT
Thus the Python function def insert(self, key, value): to insert elements into a B+ Tree was written and executed successfully.
