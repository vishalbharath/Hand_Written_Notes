A **Binary Search Tree (BST)** is a binary tree with an additional constraint:
- **Left child < Root < Right child**
- No duplicate values (usually).
- Efficient for **searching, insertion, deletion**.
- Run Time Complexity : **O(log n)**

## Inserting In a BST 

```java
    Node insert(Node root, int value) {
        if (root == null) {
            return new Node(value);
        }
        if (value < root.data) {
            root.left = insert(root.left, value);
        } else if (value > root.data) {
            root.right = insert(root.right, value);
        }
        return root;
    }
```

## Searching in a BST

```java

//SEARCHING IN BST 
class Node {
    int key;
    Node left, right;

    public Node(int item)
    {
        key = item;
        left = right = null;
    }
}
class Sample {

    // function to search a key in a BST
    static Node search(Node root, int key)
    {
        // Base Cases: root is null or key is present at
        // root
        if (root == null || root.key == key)
            return root;

        // Key is greater than root's key
        if (root.key < key)
            return search(root.right, key);

        // Key is smaller than root's key
        return search(root.left, key);
    }

    public static void main(String[] args)
    {
        
        // Creating a hard coded tree for keeping 
        // the length of the code small. We need 
        // to make sure that BST properties are 
        // maintained if we try some other cases.
        Node root = new Node(50);
        root.left = new Node(30);
        root.right = new Node(70);
        root.left.left = new Node(20);
        root.left.right = new Node(40);
        root.right.left = new Node(60);
        root.right.right = new Node(80);

        // Searching for keys in the BST
        System.out.println(search(root, 19) != null
                               ? "Found"
                               : "Not Found");
        System.out.println(search(root, 80) != null
                               ? "Found"
                               : "Not Found");
    }
}
```


## **Deletion in BST**
Cases:
1. **Node is a leaf** → Delete directly.
2. **Node has one child** → Replace node with child.
3. **Node has two children** → Replace with **inorder successor** (smallest value in right subtree).

```java
Node delete(Node root, int key) {
    if (root == null) return null;

    if (key < root.data) {
        root.left = delete(root.left, key);
    } else if (key > root.data) {
        root.right = delete(root.right, key);
    } else {
        // Case 1: No child
        if (root.left == null && root.right == null) return null;
        // Case 2: One child
        if (root.left == null) return root.right;
        if (root.right == null) return root.left;
        // Case 3: Two children
        Node successor = minValueNode(root.right);
        root.data = successor.data;
        root.right = delete(root.right, successor.data);
    }
    return root;
}

Node minValueNode(Node node) {
    Node current = node;
    while (current.left != null) {
        current = current.left;
    }
    return current;
}
```

