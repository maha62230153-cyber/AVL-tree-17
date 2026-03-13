
# AVL Tree Insertion

class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None
        self.height = 1

def height(node):
    if node is None:
        return 0
    return node.height

def balance(node):
    if node is None:
        return 0
    return height(node.left) - height(node.right)

def rightRotate(y):
    x = y.left
    t2 = x.right

    x.right = y
    y.left = t2

    y.height = max(height(y.left), height(y.right)) + 1
    x.height = max(height(x.left), height(x.right)) + 1

    return x

def leftRotate(x):
    y = x.right
    t2 = y.left

    y.left = x
    x.right = t2

    x.height = max(height(x.left), height(x.right)) + 1
    y.height = max(height(y.left), height(y.right)) + 1

    return y

def insert(node, key):
    if node is None:
        return Node(key)

    if key < node.data:
        node.left = insert(node.left, key)
    else:
        node.right = insert(node.right, key)

    node.height = 1 + max(height(node.left), height(node.right))

    b = balance(node)

    if b > 1 and key < node.left.data:
        return rightRotate(node)

    if b < -1 and key > node.right.data:
        return leftRotate(node)

    if b > 1 and key > node.left.data:
        node.left = leftRotate(node.left)
        return rightRotate(node)

    if b < -1 and key < node.right.data:
        node.right = rightRotate(node.right)
        return leftRotate(node)

    return node

def preorder(root):
    if root:
        print root.data,
        preorder(root.left)
        preorder(root.right)

root = None

n = int(raw_input("Enter number of nodes: "))
for i in range(n):
    x = int(raw_input("Enter value: "))
    root = insert(root, x)

print "Preorder traversal of AVL tree:"
preorder(root)


OUTPUT 


Enter number of nodes: 5
Enter value: 10
Enter value: 20
Enter value: 30
Enter value: 40
Enter value: 50

Preorder traversal of AVL tree:
30 20 10 40 50
