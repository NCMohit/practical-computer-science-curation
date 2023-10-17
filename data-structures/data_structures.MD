# Data Structures

## Stack
```python
class Stack:
    def __init__(self):
        self.stack = []
    def push(self,value):
        self.stack.append(value)
    def pop(self):
        return self.stack.pop()
    def top(self):
        return self.stack[-1]
```

## Queue
```python
class Queue:
    def __init__(self):
        self.q = []
    def push(self,value):
        self.q.append(value)
    def pop(self):
        res = self.q[0]
        self.q = self.q[1:]
        return res
    def top(self):
        return self.q[0]
```

## Linked Lists

### Node
```python
class Node:
    def __init__(self,value):
        self.value = value
        self.next = None
        self.prev = None
```

### Single Linked List
```python
class SingleLinkedList:
    def __init__(self):
        self.head = None
    def insert(self,val):
        if(self.head == None):
            self.head = Node(val)
        else:
            pointer = self.head
            while(pointer.next != None):
                pointer = pointer.next
            pointer.next = Node(val)
    def remove(self,val):
        pointer = self.head
        if(pointer.next == None):
            if(pointer.val==val):
                self.head = None
        while(pointer.next != None):
            if(pointer.next.val == val):
                pointer.next = pointer.next.next
                break
            pointer = pointer.next
    def reverse(self):
        left = self.head
        right = self.head.next
        left.next = None
        while(right != None):
            self.head = right
            right = self.head.next
            self.head.next = left
            left = self.head
    def traverse(self):
        pointer = self.head
        while(pointer.next != None):
            print(pointer.val,end=", ")
            pointer = pointer.next
        print(pointer.val)
```

### Double Linked List
```python
class DoubleLinkedList:
    def __init__(self):
        self.head = None
    def insert(self,val):
        if(self.head == None):
            self.head = Node(val)
        else:
            new = Node(val)
            pointer = self.head
            while(pointer.next != None):
                pointer = pointer.next
            pointer.next = new
            new.prev = pointer
    def remove(self,val):
        pointer = self.head
        if(pointer.next == None):
            if(pointer.val==val):
                self.head = None
        while(pointer.next != None):
            if(pointer.next.val == val):
                pointer.next = pointer.next.next
                pointer.next.prev = pointer
                break
            pointer = pointer.next
    def reverse(self):
        left = self.head
        right = self.head.next
        left.next = None
        while(right != None):
            self.head = right
            right = self.head.next
            self.head.next = left
            self.head.prev = right
            left = self.head
    def traverse(self):
        pointer = self.head
        while(pointer.next != None):
            print(pointer.val,end=", ")
            pointer = pointer.next
        print(pointer.val)
```

## Trees

### Node
```python
class Node:
    def __init__(self,value):
        self.value = value
        self.left = None
        self.right = None
```

### Binary Search Tree
```python
class BST:
    def __init__(self):
        self.root = None
    def insert(self,value):
        if(self.root == None):
            self.root = Node(value)
            return None
        pointer = self.root
        while(True):
            if(pointer.value < value):
                if(pointer.right != None):
                    pointer = pointer.right
                else:
                    pointer.right = Node(value)
                    break
            else:
                if(pointer.left != None):
                    pointer = pointer.left
                else:
                    pointer.left = Node(value)
                    break
    def search(self,value):
        pointer = self.root
        exists = 0
        path = []
        while(pointer!=None):
            path.append(pointer.value)
            if(pointer.value == value):
                exists = 1
                break
            elif(pointer.value < value):
                pointer = pointer.right
                path.append("right")
            else:
                pointer = pointer.left
                path.append("left")
        return [exists,path]
    def inorder_traversal(self,node):
        if(node!=None):
            left = self.inorder_traversal(node.left)
            center = [node.value]
            right = self.inorder_traversal(node.right)
            return left+center+right
        else:
            return []
    def preorder_traversal(self,node):
        if(node!=None):
            left = self.inorder_traversal(node.left)
            center = [node.value]
            right = self.inorder_traversal(node.right)
            return center+left+right
        else:
            return []
    def postorder_traversal(self,node):
        if(node!=None):
            left = self.inorder_traversal(node.left)
            center = [node.value]
            right = self.inorder_traversal(node.right)
            return left+right+center
        else:
            return []
```

## Graphs
```python
class Graph:
    def __init__(self,vertices,edges):
        self.vertices = vertices    # List of vertices ["A","B","C"]
        self.edges = edges          # Dictionary of edges {"A":"B" , "B":"C"}
    def get_neighbours(self,vertex):
        neighbors = []
        for edge in self.edges.items():
            if(edge[0]==vertex):
                if(edge[1] not in neighbors):
                    neighbors.append(edge[1])
            elif(edge[1]==vertex):
                if(edge[0] not in neighbors):
                    neighbors.append(edge[0])
        return neighbors
    def depth_first_search(self,start_vertex,find_vertex):
        stack = Stack()
        visited = [start_vertex]
        stack.push(start_vertex)
        path_exists = 0
        path = []
        while(len(stack.stack)!=0):
            neighbors = self.get_neighbours(stack.stack[-1])
            removal = []
            for neighbor in neighbors:
                if(neighbor in visited):
                    removal.append(neighbor)
            for x in removal:
                neighbors.remove(x)
            if(len(neighbors)!=0):
                stack.push(neighbors[0])
                visited.append(neighbors[0])
                if(neighbors[0]==find_vertex):
                    path = stack.stack.copy()
                    path_exists = 1
            else:
                stack.pop()
        return [path_exists,path]
    def breadth_first_search(self,start_vertex,find_vertex):
        q = Queue()
        visited = [start_vertex]
        q.push(start_vertex)
        path_exists = 0
        while(len(q.q)!=0):
            neighbors = self.get_neighbours(q.q[0])
            q.pop()
            removal = []
            for neighbor in neighbors:
                if(neighbor in visited):
                    removal.append(neighbor)
            for x in removal:
                neighbors.remove(x)
            if(len(neighbors)!=0):
                for neighbor in neighbors:
                    q.push(neighbor)
                    visited.append(neighbor)
                    if(neighbor==find_vertex):
                        path_exists = 1
            else:
                q.pop()
        return path_exists  
```