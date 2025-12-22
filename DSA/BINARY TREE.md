A **binary tree** is a hierarchical data structure where:
- Each node has **at most two children**:
    - **Left child**
    - **Right child**
Special properties:
- A tree with `n` nodes has `n-1` edges.
- Height = longest path from root to leaf.
- Depth of a node = distance from root.
```java
//NODE STRUCTURE
class Node {
    int data;
    Node left, right;

    Node(int value) {
        data = value;
        left = right = null;
    }
}
```

```java
//binary tree class
class BinaryTree {
    Node root;

    BinaryTree() {
        root = null;
    }
}
```

## Traversals in a Binary Tree

### Inorder Traversal (Left → Root → Right)

```java
void inorder(Node node) {
    if (node == null) return;
    inorder(node.left);
    System.out.print(node.data + " ");
    inorder(node.right);
}
```

### Preorder (Root → Left → Right)

```java
void preorder(Node node) {
    if (node == null) return;
    System.out.print(node.data + " ");
    preorder(node.left);
    preorder(node.right);
}
```

### Postorder (Left → Right → Root)

```java
void postorder(Node node) {
    if (node == null) return;
    postorder(node.left);
    postorder(node.right);
    System.out.print(node.data + " ");
}
```


![[Pasted image 20250824130116.png]]![[Pasted image 20250824130129.png]]